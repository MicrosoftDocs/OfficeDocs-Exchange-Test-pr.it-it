---
title: 'Utilizzare le regole di flusso di posta elettronica in modo che i messaggi possono ignorare confusione: Exchange 2013 Help'
TOCTitle: Utilizzare le regole di flusso di posta elettronica in modo che i messaggi possono ignorare confusione
ms:assetid: 58e413f0-aa27-4307-bffd-4df03090a15e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn896639(v=EXCHG.150)
ms:contentKeyID: 64380508
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzare le regole di flusso di posta elettronica in modo che i messaggi possono ignorare confusione

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Se si desidera essere certi di ricevere messaggi specifici, è possibile creare una regola di trasporto di Exchange che assicura che questi messaggi ignorino la cartella di confusione. Estrarre [Confusione utilizzare per ordinare i messaggi con priorità bassa in Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=528411) per ulteriori informazioni su confusione.

Per altre attività di gestione correlate alle regole di trasporto, vedere l'argomento di PowerShell [New-TransportRule](https://technet.microsoft.com/it-it/library/bb125138\(v=exchg.150\)) and [Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) . Se ha familiarità con PowerShell, vedere gli argomenti seguenti per informazioni sull'utilizzo di Powershell:

  - [Connessione a Exchange Online tramite Remote PowerShell](https://technet.microsoft.com/it-it/library/jj984289\(v=exchg.150\))

  - [Connessione a Exchange tramite shell remota](https://technet.microsoft.com/it-it/library/dd335083\(v=exchg.150\))

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Regole di trasporto" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Utilizzare l'interfaccia Utente per creare una regola di trasporto per ignorare la cartella confusione

Questo esempio consente a tutti i messaggi con titolo "Riunione" evitare confusione.

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **flusso di posta** \> **regole**. Fare clic su ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e quindi fare clic su **Crea una nuova regola...**.

2.  Una volta terminate la creazione della nuova regola, fare clic su **Salva** per avviare la regola.

![Esempio immagine: Se nell'oggetto è contenuta la riunione, ignorare i messaggi secondari](images/Dn896639.75957aa4-4b2a-4142-92ff-07f8ccc64d82(EXCHG.150).png "Esempio immagine: Se nell'oggetto è contenuta la riunione, ignorare i messaggi secondari")

## Utilizzo della Shell per creare una regola di trasporto per ignorare la cartella di confusione

Questo esempio consente a tutti i messaggi con titolo "Riunione" evitare confusione.

    New-TransportRule -Name <name_of_the_rule> -SubjectContainsWords "Meeting" -SetHeaderName "X-MS-Exchange-Organization-BypassClutter" -SetHeaderValue "true"


> [!IMPORTANT]
> In questo esempio, "X-MS-Exchange-organizzazione-BypassClutter" e "true" viene fatta distinzione tra maiuscole e minuscole.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-TransportRule](https://technet.microsoft.com/it-it/library/bb125138\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

È possibile controllare le intestazioni dei messaggi di posta elettronica per verificare se i messaggi di posta elettronica sono di destinazione nella posta in arrivo a causa della regola di trasporto confusione bypass. Selezionare un messaggio di posta elettronica da una cassetta postale nell'organizzazione con più chiara la visualizzazione della regola di trasporto applicata il bypass. Esaminare le intestazioni indicate sul messaggio e verrà visualizzato il **X-MS-Exchange-organizzazione-BypassClutter: true** intestazione. Di conseguenza, che il bypass sta funzionando. Leggere l'argomento [Visualizza le informazioni di intestazione Internet per un messaggio di posta elettronica](https://go.microsoft.com/fwlink/p/?linkid=822530) per informazioni su come trovare le informazioni di intestazione.


> [!NOTE]
> Gli elementi del calendario, simili alle riunioni accettati, inviato o rifiutata non disporrà di queste intestazioni su di essi. Si impegna in estensione delle funzionalità confusione questi elementi di calendario presto disponibili.



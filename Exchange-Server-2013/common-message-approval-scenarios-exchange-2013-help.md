---
title: 'Scenari comuni di approvazione messaggio: Exchange 2013 Help'
TOCTitle: Scenari comuni di approvazione messaggio
ms:assetid: 5c13a07e-c21d-4502-a9f9-fb801197e1dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298007(v=EXCHG.150)
ms:contentKeyID: 50480762
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Scenari comuni di approvazione messaggio

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-09-29_

L'organizzazione potrebbe essere necessario approvare le determinati tipi di messaggi per soddisfare i requisiti legati o di conformità o per implementare un flusso di lavoro aziendali specifici. Di seguito sono riportati alcuni esempi di scenari comuni che è possibile impostare utilizzando Exchange:

  - Nell'esempio 1: Evitare tempeste di posta elettronica a un gruppo di distribuzione di grandi dimensioni

  - Nell'esempio 2: Inoltrare i messaggi al responsabile del mittente per approvazione

  - Nell'esempio 3: Configurare una catena di approvazione del messaggio

  - Nell'esempio 4: Inoltrare i messaggi che soddisfano uno dei diversi criteri

  - Nell'esempio 5: Inoltrare un messaggio che contiene informazioni riservate

## Nell'esempio 1: Evitare tempeste di posta elettronica a un gruppo di distribuzione di grandi dimensioni

Per controllare i messaggi a un gruppo di distribuzione di grandi dimensioni, è possibile richiedere che un moderatore approvare i messaggi inviati a tale gruppo. Se non esistono criteri per i quali i messaggi richiedono l'approvazione, il modo più semplice configurazione consiste nel configurare il gruppo per richiedere l'approvazione del messaggio.

In questo esempio tutti i messaggi al gruppo di tutti i dipendenti devono essere approvati, tranne se i mittenti sono membri del gruppo di distribuzione denominato Team legale.

![Impostazioni messaggio di approvazione per un gruppo di distribuzione](images/Dd298007.77721509-93f9-4a90-8d77-986db2b0acf4(EXCHG.150).png "Impostazioni messaggio di approvazione per un gruppo di distribuzione")

Per richiedere che i messaggi a un gruppo di distribuzione specifici approvare, nell'interfaccia di amministrazione di Exchange (EAC), andare a **destinatari** \> **gruppi**, modificare il gruppo di distribuzione e quindi selezionare **approvazione del messaggio**.

## Nell'esempio 2: Inoltrare i messaggi al responsabile del mittente per approvazione

Ecco alcuni tipi comuni di messaggi per il quale è possibile richiedere l'approvazione del responsabile:

  - Messaggi inviati da un utente a determinati gruppi di distribuzione o destinatari

  - Messaggi inviati a utenti esterni o partner

  - Messaggi inviati tra due gruppi

  - Messaggi inviati con contenuto specifico, ad esempio il nome di un cliente specifico

  - Messaggi inviati da un utente del training

Per richiedere inviato un messaggio per l'approvazione, per prima cosa, creare una regola mediante il modello di **inviare messaggi a un moderatore** e selezionare i messaggi devono accedere al responsabile del mittente, come illustrato nella schermate seguenti.

![Utilizzo di un modello per creare la nuova regola](images/Dd298007.051a5653-1a09-4db4-908f-48b56cc8d13f(EXCHG.150).png "Utilizzo di un modello per creare la nuova regola")

Quindi, definire i messaggi che necessaria l'approvazione.

Di seguito è riportato un esempio in cui tutti i messaggi inviati da un utente del training, Garth Fort a destinatari esterni all'organizzazione richiede l'approvazione del responsabile.

![Regola che inoltra i messaggi al manager dell'utente](images/Dd298007.7f94c22e-b5ba-45a3-9ccd-31996b6c863a(EXCHG.150).png "Regola che inoltra i messaggi al manager dell'utente")

Per iniziare, passare a EAC \> **flusso di posta** \> **regole** e creare una nuova regola utilizzando il modello di **inviare messaggi a un moderatore**.


> [!IMPORTANT]
> Alcune condizioni e azioni, compresa l'inoltro al responsabile del mittente, sono nascosto per impostazione predefinita nella pagina <STRONG>nuova regola</STRONG>. Per visualizzare tutte le condizioni e azioni, selezionare <STRONG>altre opzioni</STRONG>.



## Nell'esempio 3: Configurare una catena di approvazione del messaggio

È possibile richiedere più livelli di approvazione per i messaggi. Ad esempio, è possibile richiedere che i messaggi per un cliente specifico vengano approvate prima da un gestore di relazione cliente e quindi da un responsabile della conformità oppure è possibile richiedere che possibile approvare le spese per due livelli di Manager.

Per creare questo tipo di approvazione di più livelli, creare una regola di trasporto per ogni livello di approvazione. Ogni regola rileva gli stessi modelli di messaggi, come indicato di seguito:

  - La prima regola inoltra il messaggio al responsabile approvazione prima. Quando il primo approvatore accetta il messaggio, il messaggio passa automaticamente al responsabile approvazione nella seconda regola.

  - Se tutti i responsabili approvazione nella catena selezionare **Approva** quando ricevono la richiesta di approvazione, al termine dell'ultima approvazione nella catena, il messaggio originale viene inviato al destinatario.

  - Se tutti gli utenti nella catena di approvazione seleziona **rifiutare** quando ricevono la richiesta di approvazione, il mittente riceve un messaggio di rifiuto.

  - Se uno dei approvazione richieste non vengono approvate entro il tempo di scadenza (2 giorni per Exchange Online, 5 giorni per Exchange Server 2013 ), il mittente riceve un messaggio di scadenza.

Nell'esempio seguente si presuppone che è un cliente di Blue Yonder Airlines che si desidera che il gestore delle relazioni dei clienti e responsabile della conformità per approvare tutti i messaggi inviati a questo cliente. Creare due regole, uno per ogni revisore. La prima regola viene inoltrata al responsabile approvazione di primo livello. La seconda regola viene inoltrata al responsabile approvazione secondo livello.

![Due regole utilizzate per due livelli di approvazione](images/Dd298007.29686c05-eaa0-42b9-86ad-d577f656392c(EXCHG.150).png "Due regole utilizzate per due livelli di approvazione")

La prima regola identifica tutti i messaggi con il nome della società Blue Yonder Airlines nell'oggetto o del messaggio e invia i messaggi per il gestore delle relazioni clienti interni di Blue Yonder Airlines, Garret Vargas.

![Regola per il revisore di primo livello](images/Dd298007.e22d1c04-85c5-4227-88e6-b118d5593350(EXCHG.150).png "Regola per il revisore di primo livello")

La seconda regola invia questi messaggi per il responsabile della conformità, Tony Krijnen.

![Regola di approvazione di secondo livello, con gli stessi criteri](images/Dd298007.5d888786-8e48-4459-ab86-8a4b9a016d58(EXCHG.150).png "Regola di approvazione di secondo livello, con gli stessi criteri")

## Nell'esempio 4: Inoltrare i messaggi che soddisfano uno dei diversi criteri

All'interno di una regola di trasporto, devono essere soddisfatte per la regola da soddisfare tutte le condizioni configurate all'interno della regola. Se si desidera che le stesse operazioni applicate per entrambe le condizioni, è consigliabile creare una regola separata per ognuno.

A tale scopo, nella pagina **regole** di amministrazione di Exchange, creare una regola per la prima condizione. Selezionare la regola, scegliere **Copia** e modificare le condizioni nella nuova regola da soddisfare le condizioni secondo.

Prestare attenzione quando si tenta di creare più regole con condizioni "O" in modo che non verrà visualizzata con un messaggio da inviare più volte al responsabile approvazione. Per evitare questo problema, aggiungere un'eccezione per la seconda regola in modo e Ignora messaggi corrispondenti alla prima regola.

Ad esempio, una sola regola non è controllerà se un messaggio contiene "offerta di vendita" nell'oggetto del o del titolo di allegati. Per evitare il messaggio da inviare più volte al responsabile approvazione, se la prima regola controlli "offerta di vendita" nell'oggetto o nel corpo del messaggio, un'eccezione che contiene criteri la prima regola è necessario che la seconda regola che consente di controllare "offerta di vendita" nel contenuto dell'allegato.

![Utilizzo di un'eccezione per la seconda regola](images/Dd298007.c39bbdcf-c619-4f84-8922-114ad1da824d(EXCHG.150).png "Utilizzo di un'eccezione per la seconda regola")


> [!NOTE]
> Eccezioni sono nascosto per impostazione predefinita nella pagina <STRONG>nuova regola</STRONG>. Per visualizzare tutte le condizioni e azioni, selezionare <STRONG>altre opzioni</STRONG>.



## Nell'esempio 5: Inoltrare un messaggio che contiene informazioni riservate

Se si dispone di funzionalità [Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)(DLP), sono predefiniti molti altri tipi di informazioni riservate. Con DLP, vedere che il messaggio contiene una condizione di informazioni riservate. Se si dispone di DLP, è possibile creare le condizioni che identificano i modelli di informazioni riservate specifiche che sono univoche per l'organizzazione.

Di seguito è riportato un esempio in messaggi di informazioni sensibili richiedono l'approvazione. In questo esempio, i messaggi che contengono un numero di carta di credito richiedono l'approvazione.

![Regola che inoltra la posta con informazioni riservate](images/Dd298007.7ec1ca74-5d20-42ea-a9ee-3a8b25beb7df(EXCHG.150).png "Regola che inoltra la posta con informazioni riservate")

## Vedere anche


[Gestione approvazione del messaggio](manage-message-approval-exchange-2013-help.md)


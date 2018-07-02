---
title: 'Consentire agli utenti di posta elettronica di inoltrare le chiamate vocali: Exchange 2013 Help'
TOCTitle: Consentire agli utenti di posta elettronica di inoltrare le chiamate vocali
ms:assetid: 1f8e0a53-3d9d-4f8c-9be3-9f1e2a4347a3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335138(v=EXCHG.150)
ms:contentKeyID: 50555553
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire agli utenti di posta elettronica di inoltrare le chiamate vocali

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

La funzionalità Regole ricezione chiamata è stata inizialmente introdotta in Exchange 2010. Utilizzando questa funzionalità, per gli utenti abilitati all'utilizzo della casella vocale è possibile controllare in che modo dovrebbero essere gestite le chiamate in arrivo. Le regole di ricezione chiamata vengono applicate alle chiamate in arrivo in modo simile a quello in cui le Regole posta in arrivo vengono applicate ai messaggi di posta in arrivo.

Le regole di ricezione chiamata vengono create e configurate da un utente abilitato all'uso della casella vocale tramite Outlook o Outlook Web App. Le regole sono memorizzate insieme ad altre impostazioni vocali nella cassetta postale dell'utente. Per ciascuna cassetta postale abilitata alla messaggistica unificata è possibile impostare un totale di nove regole di ricezione chiamata. Queste regole sono indipendenti da Regole posta in arrivo configurate dagli utenti e non occupano una parte della quota di archiviazione delle regole della posta in arrivo per l'utente.

Per impostazione predefinita, quando un utente viene abilitato all'utilizzo della messaggistica unificata e della casella vocale non viene configurata nessuna regola di ricezione chiamata. Se a una chiamata in arrivo risponde il sistema di caselle vocali, al chiamante viene richiesto di lasciare un messaggio vocale o se al chiamante non viene fatta alcuna richiesta, gli sarà comunque possibile lasciare un messaggio vocale per l'utente.

Se gli utenti desiderano che il sistema di caselle vocali risponda solo alle chiamate in arrivo e registri un messaggio vocale, non è necessario creare alcuna regola di ricezione chiamata. Tuttavia, se si desiderano configurare condizioni o azioni, è possibile configurarle utilizzando la sezione **Regole di ricezione chiamata** nella pagina **Sistema di caselle vocali** in Outlook Web App. Utilizzare la sezione **Regole di ricezione chiamata**, per creare, modificare ed eliminare le regole di ricezione chiamata.

## Analisi delle regole di ricezione chiamata

Una regola per il risponditore automatico è costituita da due parti: condizioni e azioni. È possibile associare una o più condizioni a una singola regola per il risponditore automatico. La regola per il risponditore automatico verrà elaborata solo se ne sono soddisfatte tutte le condizioni. È inoltre possibile associare una o più azioni a una singola regola per il risponditore automatico. Le azioni definiscono quali opzioni saranno disponibili al chiamante una volta elaborata la regola.

Le regole di ricezione chiamata si basano sulle seguenti condizioni:

  - Chiamante

  - Ora del giorno

  - Stato della disponibilità calendario

  - Attivazione delle risposte automatiche per i messaggi di posta elettronica

Sono disponibili le seguenti azioni:

  - Numeri alternativi

  - Trasferimento del chiamante a un altro utente

  - Registrazione di un messaggio vocale

Se un utente registra un messaggio di saluto personalizzato per una regola per il risponditore automatico, dovrà includere l'opzione di menu nel messaggio quando configura la regola. In caso contrario, Messaggistica unificata non genererà una richiesta di menu per far sapere al chiamante quali siano le sue scelte. Dopo la riproduzione del messaggio di saluto personalizzato, il server attende la risposta del chiamante. Se un'opzione di menu non è stata inserita nel messaggio di saluto, il chiamante non fornirà alcuna risposta e il server chiederà al chiamante se è ancora in linea.

## Condizioni

Le condizioni sono regole applicabili alle regole di ricezione chiamata. Utilizzando una combinazione di condizioni, è possibile creare più regole di ricezione chiamata attivabili quando le condizioni vengono soddisfatte. Per creare una regola predefinita da applicare a tutte le chiamate, si crea una regola che non contiene alcuna condizione.

Le condizioni da utilizzare quando si configurano le regole di ricezione chiamata sono tre:

  - ID chiamante

  - Ora

  - Stato della disponibilità

## Azioni

Le azioni vengono utilizzate per definire cosa accade quando una condizione viene soddisfatta. Le azioni sono di due tipi:

  - Numeri alternativi

  - Trasferimento chiamata

**Aggiunta di un'azione Trovami**

Quando un chiamante seleziona l'opzione Trovami, il sistema di caselle vocali tenterà di individuare l'utente fino a un massimo di due numeri di telefono e di connettere il chiamante all'utente, se quest'ultimo è disponibile a uno dei numeri di telefono.

  - È possibile specificare il testo da leggere al chiamante. Ad esempio, se si immette "Questioni urgenti" per informare i chiamanti che devono selezionare questa azione solo se devono discutere di questioni importanti, il sistema di caselle vocali dirà: "Per questioni urgenti, premere il tasto 1."

  - È necessario associare l'azione Trovami al numero sulla tastiera del telefono che il chiamate dovrà premere per selezionare l'azione. Nell'esempio precedente, **1** è il tasto del telefono che i chiamanti premeranno per contattare l'utente a uno dei numeri di telefono specificati.

  - Quindi, è necessario specificare uno o due numeri di telefono che verranno chiamati dal sistema di caselle vocali. Se si specificano due numeri di telefono, il secondo verrà composto nel caso in cui non si risulti disponibile al primo. Ogni numero di telefono specificato dispone di una durata associata. La durata indica il periodo di tempo durante cui il sistema di caselle vocali tenterà di comporre il numero di telefono prima di passare al numero successivo. Oppure, se non è possibile contattare l'utente, il sistema di caselle vocali tornerà al menu delle opzioni.

  - Una volta immesse queste informazioni, fare clic su **Applica** per salvare le impostazioni Trovami.

**Aggiunta delle azioni di trasferimento chiamata**

Impostando l'azione Trasferimento di chiamata, si fornisce ai chiamanti l'opzione di essere trasferiti al numero di telefono di un'altra persona. Esistono diverse opzioni disponibili quando si desidera trasferire una chiamata in arrivo a un altro telefono o contatto.

  - È possibile specificare il testo da leggere al chiamante. Ad esempio, è possibile immettere \&quot;Questioni importanti\&quot; per informare i chiamanti che devono scegliere questa opzione se desiderano discutere di una questione importante con qualcuno.

  - È necessario associare l'azione **Trasferimento di chiamata** al numero sulla tastiera del telefono che il chiamante premerà per selezionare l'azione.

  - Quando si sceglie l'azione Trasferimento di chiamata, è necessario specificare una persona o un numero di telefono a cui trasferire il chiamante. È possibile scegliere un numero di telefono o selezionare un contatto da chiamare quando il chiamante preme il tasto corretto sulla tastiera del telefono. Se si specifica un contatto all'interno della directory aziendale, il sistema di caselle vocali tenterà di trasferire la chiamata al numero di interno del contatto.

  - Oltre a specificare una persona o un numero a cui trasferire il chiamante, è necessario specificare anche il numero sulla tastiera del telefono che il chiamante dovrà premere per selezionare l'azione Trasferimento di chiamata.

  - Una volta immesse queste informazioni, fare clic su **Applica** per salvare le impostazioni Trasferimento di chiamata.

## Selezione di una regola per il risponditore automatico per ogni chiamata in arrivo

Dopo che saranno state create e configurate le regole per il risponditore automatico, Messaggistica unificata:

1.  Verificare se l'utente ha creato eventuali regole per il risponditore automatico. In caso contrario, Messaggistica unificata offrirà al chiamante la possibilità di lasciare un messaggio vocale.

2.  Se sono state configurate una o più regole risponditore automatico, Messaggistica unificata le valuterà una per una. Verrà elaborata la prima regola le cui condizioni sono soddisfatte.

3.  Dopo la valutazione di tutte le regole, se Messaggistica unificata non trova una regola le cui condizioni sono soddisfatte, chiede al chiamante di lasciare una messaggio vocale.

## Regole di composizione

In base alla configurazione di una regola per risponditore automatico, la chiamata in arrivo può essere trasferita. In tal caso, il numero di telefono a cui viene trasferita la chiamata sarà soggetto alle regole di composizione e alle restrizioni stabilite dai criteri di messaggistica unificata a cui è associato il chiamato. Per ulteriori informazioni sulle regole di composizione e di chiamate esterne e sulle limitazioni, vedere [Consentire agli utenti di effettuare chiamate](allow-users-to-make-calls-exchange-2013-help.md).

## Abilitazione/disabilitazione delle regole di ricezione chiamata

Per impostazione predefinita, le regole di ricezione chiamata sono abilitate automaticamente per gli utenti abilitati alla messaggistica unificata. È comunque possibile disabilitare le regole di ricezione chiamata disabilitandone la funzionalità su un criterio cassetta postale di messaggistica unificata o sulla cassetta postale dell'utente. Per i dettagli su come abilitare o disabilitare le regole di ricezione chiamata, vedere i seguenti argomenti:

  - [Consentire o impedire agli utenti gli stessi criteri cassetta postale di messaggistica unificata di creazione di regole di ricezione chiamata](allow-or-prevent-users-in-the-same-um-mailbox-policy-from-creating-call-answering-rules-exchange-2013-help.md)

  - [Consentire o impedire a un utente di creare regole di ricezione chiamata](allow-or-prevent-a-user-from-creating-call-answering-rules-exchange-2013-help.md)


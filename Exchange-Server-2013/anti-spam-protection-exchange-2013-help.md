---
title: 'Protezione anti-spam: Exchange 2013 Help'
TOCTitle: Protezione anti-spam
ms:assetid: 6af88a08-687d-40b1-8b22-80704184403d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ218660(v=EXCHG.150)
ms:contentKeyID: 50480825
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Protezione anti-spam

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-06_

*Invio di posta indesiderata*o messaggi dannosi, utilizzano una serie di tecniche per inviare posta indesiderata nella propria organizzazione. Nessun singolo strumento o processo consente di eliminare tutta la posta indesiderata. Tuttavia, Microsoft Exchange Server 2013 fornisce un approccio più livelli, ramificazioni e articolato riduzione questi messaggi indesiderati. Exchange utilizza gli agenti di trasporto per fornire protezione da posta indesiderata e gli agenti predefiniti disponibili in Exchange 2013 rimangono invariati relativamente da Microsoft Exchange Server 2010.

Per ulteriori funzionalità di protezione da posta indesiderata e semplifica la gestione, è possibile scegliere di acquistare Microsoft Exchange Online Protection (EOP). Per un confronto delle funzionalità di EOP e Exchange 2013, vedere [Vantaggi delle funzionalità antivirus in Exchange Online Protection su Exchange Server 2013](benefits-of-anti-spam-features-in-exchange-online-protection-over-exchange-server-2013-exchange-2013-help.md). Per ulteriori informazioni sulla protezione anti-spam Office 365, vedere [Office 365 posta Anti-Spam Protection](https://support.office.com/en-us/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us).

Per informazioni sulle funzionalità antimalware incorporate in Exchange 2013, vedere [Protezione antimalware](anti-malware-protection-exchange-2013-help.md).

**Sommario**

Anti-spam agents on Mailbox servers

Anti-spam agents on Edge Transport servers

Anti-spam stamps

Strategy for anti-spam approach

## Agenti di protezione dalla posta indesiderata sui server Cassette postali

Generalmente, gli agenti di protezione dalla posta indesiderata vengono abilitati su un server Cassette postali se l'organizzazione non dispone di un server Trasporto Edge o non esegue alcun filtraggio prima di accettare i messaggi in ingresso. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

Come a tutti gli agenti di trasporto, anche agli agenti di protezione dalla posta indesiderata è assegnata una priorità. Un valore più basso indica una priorità più alta e di conseguenza un agente di protezione con priorità 1 agirà su un messaggio prima di un agente con priorità 9. Tuttavia, anche l'evento SMTP in cui viene registrato l'agente di protezione dalla posta indesiderata è importante per stabilire l'ordine di azione degli agenti sui messaggi. Un agente con priorità più bassa registrato in un evento SMTP precedente nella pipeline di trasporto agirà su un messaggio prima di un agente con una priorità più alta ma che è stato registrato in un evento SMTP successivo nella pipeline.

Nel seguente elenco sono indicati gli agenti di protezione dalla posta indesiderata e il loro ordine predefinito di applicazione ai messaggi su un server Cassette postali sulla base del valore di priorità predefinito dell'agente e dell'evento SMTP nella pipeline di trasporto in cui è registrato:

1.  **Agente filtro mittente**   Il filtro mittente confronta il mittente nel comando SMTP MAIL FROM: SMTP con un elenco definito dall'amministratore di mittenti a cui è vietato inviare messaggi all'organizzazione per determinare l'eventuale azione da intraprendere su un messaggio in ingresso. Per ulteriori informazioni, vedere [Filtro mittente](sender-filtering-exchange-2013-help.md).

2.  **Agente ID mittente**   L'ID mittente si basa sull'indirizzo IP del server di invio e sul Purported Responsible Address (PRA) del mittente per stabilire se quest'ultimo è contraffatto o meno. Per ulteriori informazioni, vedere [ID mittente](sender-id-exchange-2013-help.md).

3.  **Agente filtro contenuto**   Il filtro del contenuto valuta il contenuto di un messaggio. Per ulteriori informazioni, vedere [Filtro contenuto](content-filtering-exchange-2013-help.md).
    
    La quarantena della posta indesiderata è una funzione dell'agente filtro contenuto che riduce il rischio di perdita di messaggi legittimi erroneamente classificati come posta indesiderata. Questa funzionalità fornisce un percorso di archiviazione temporanea per i messaggi identificati come posta indesiderata che non devono essere recapitati alla cassetta postale di un utente all'interno dell'organizzazione. Per ulteriori informazioni, vedere [Quarantena posta indesiderata](spam-quarantine-exchange-2013-help.md).
    
    Inoltre, il filtro contenuto agisce sulla funzionalità di aggregazione dell'elenco indirizzi attendibili. L'aggregazione dell'elenco di indirizzi attendibili consente di raccogliere i dati dagli elenchi di indirizzi protetti dalla posta indesiderata che gli utenti di Microsoft Outlook e Outlook Web App configurano e rendere tali dati disponibili per l'agente filtro contenuto. Per ulteriori informazioni, vedere [Aggregazione dell'elenco indirizzi attendibili](safelist-aggregation-exchange-2013-help.md).

4.  **Agente di analisi protocollo**   L'agente di analisi protocollo implementa la funzionalità di reputazione dei mittenti. La reputazione del mittente si basa sui dati permanenti dell'indirizzo IP del server di invio per stabilire l'eventuale azione da intraprendere su un messaggio in ingresso. Il livello di reputazione mittente (SRL, Sender Reputation Level) viene calcolato da diverse caratteristiche del mittente derivate dall'analisi del messaggio e da verifiche esterne. Per ulteriori informazioni, vedere [Reputazione mittente e agente di analisi protocollo](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md).

Inizio pagina

## Anti-spam agents on Edge Transport servers

Se l'organizzazione dispone di un server Trasporto Edge installato nella rete perimetrale, tutti gli agenti protezione da posta indesiderati che sono disponibili su un server cassette postali è installati e abilitati per impostazione predefinita nei server Trasporto Edge. Tuttavia, gli agenti protezione da posta indesiderati seguenti sono disponibili solo in un server Trasporto Edge:

  - **Agente filtro connessioni**   Il filtro connessioni controlla l'indirizzo IP del server remoto che tenta di inviare messaggi per determinare quale azione, se presente, deve essere eseguita su un messaggio in ingresso. Il filtro connessioni utilizza un elenco di indirizzi IP bloccati, elenco indirizzi IP consentiti, servizi provider elenco indirizzi IP bloccati e servizi del provider elenco indirizzi IP consentiti per determinare se IP della connessione devono essere bloccata o consentita. Per ulteriori informazioni, vedere [Il filtro connessioni su server Trasporto Edge](connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

  - **Agente filtro destinatario**   Il filtro destinatario confronta i destinatari del messaggio nel comando SMTP RCPT TO: SMTP con un elenco di destinatari bloccati definito dall'amministratore. Se viene rilevata una corrispondenza, il messaggio non può accedere all'organizzazione. Il filtro destinatario confronta i destinatari dei messaggi in ingresso anche con una directory dei destinatari locale per stabilire se il messaggio è indirizzato a destinatari validi. Quando un messaggio non è indirizzato a destinatari validi, viene rifiutato. Per ulteriori informazioni, vedere [Filtro destinatari nei server Trasporto Edge](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).
    

    > [!NOTE]
    > Anche se l'agente filtro destinatario è disponibile nei server cassette postali, è consigliabile non configurarlo. Quando il filtro destinatario su un server cassette postali rileva un destinatario non valido o bloccato in un messaggio che contiene gli altri destinatari validi, il messaggio viene rifiutato. Se si installa gli agenti protezione da posta indesiderati in un server cassette postali, l'agente filtro destinatario è abilitata per impostazione predefinita. Tuttavia, quest'ultimo non è configurato per bloccare tutti i destinatari.



  - **Agente filtro allegati**   Il filtro degli allegati Blocca messaggi in base al nome del file allegato, estensione di file o tipo di contenuto MIME di file. È possibile configurare per bloccare il messaggio e il relativo allegato, per rimuovere l'allegato e consentire il messaggio superare o eliminare il messaggio e il relativo allegato del filtro degli allegati. Per ulteriori informazioni, vedere [Filtro degli allegati nei server Trasporto Edge](attachment-filtering-on-edge-transport-servers-exchange-2013-help.md).

Di seguito è riportato l'ordine predefinito di applicazione degli agenti di protezione dalla posta indesiderata sul server Trasporto Edge sulla base del valore di priorità predefinito dell'agente e dell'evento SMTP nella pipeline di trasporto in cui è registrato:

1.  Agente filtro connessioni

2.  Agente filtro mittente

3.  Agente Filtro destinatario

4.  Agente ID mittente

5.  Agente filtro contenuto

6.  Agente di analisi protocollo per reputazione mittente

7.  Agente di filtro degli allegati

Inizio pagina

## Contrassegni filtro posta indesiderata

Gli indicatori di protezione da posta indesiderata permettono di effettuare una diagnosi dei problemi relativi alla posta indesiderata applicando i metadati diagnostici o gli indicatori, come le informazioni specifiche sul mittente, i risultati della convalida puzzle e di filtro contenuto, ai messaggi quando passano attraverso le funzionalità di protezione da posta indesiderata che filtrano i messaggi in ingresso da Internet. Per ulteriori informazioni, vedere [Contrassegni filtro posta indesiderata](anti-spam-stamps-exchange-2013-help.md).

Inizio pagina

## Strategia per la protezione dalla posta indesiderata

La strategia di configurazione delle funzionalità di protezione da posta indesiderata e di definizione dell'aggressività delle impostazioni dell'agente di protezione da posta indesiderata richiede una pianificazione e un calcolo accurati. Se tutti i filtri di protezione da posta indesiderata vengono impostati ai livelli più alti e configurati per il rifiuto di tutti i messaggi sospetti, è più probabile che vengano rifiutati i messaggi non indesiderati. Al contrario, se i filtri di protezione da posta indesiderata non vengono impostati a un livello sufficientemente alto e la soglia del livello di probabilità di posta indesiderata a un livello sufficientemente basso, probabilmente non si verificherà una riduzione nella quantità di posta indesiderata che accede all'organizzazione.

Si consiglia di rifiutare un messaggio quando Exchange rileva un problema con il messaggio tramite l'agente filtro connessioni, filtro destinatari o filtro mittente. Questo approccio è migliore rispetto alla messa in quarantena dei messaggi o all'assegnazione di metadati, quali contrassegni di protezione da posta indesiderata, a questi messaggi. Gli agenti filtro connessioni e filtro destinatari bloccano automaticamente i messaggi identificati dai rispettivi filtri. L'agente filtro mittente può essere configurato.

Questa procedura è consigliata poiché il livello di probabilità di posta indesiderata su cui si basano il filtro connessioni, il filtro destinatari o il filtro mittente è relativamente alto. Ad esempio, se l'amministratore ha configurato il blocco di mittenti specifici nel filtro mittente, non è necessario associare i dati relativi al filtro mittente a tali messaggi e continuare a elaborarli. Nella maggior parte delle organizzazioni, i messaggi bloccati vengono rifiutati. (Se non si desidera rifiutarli, non occorre inserire i messaggi nell'elenco Mittenti bloccati.)

La stessa logica viene applicata ai servizi relativi all'elenco indirizzi bloccati in tempo reale e al filtro destinatari, anche se il livello di protezione su cui si basano non è così alto come quello dell'elenco indirizzi IP bloccati. Più in profondità un messaggio viene trasmesso nel percorso del flusso di posta, più alta è la probabilità di falsi positivi, poiché le funzionalità di protezione da posta indesiderata valutano più variabili. Pertanto, si noterà che configurando le prime funzionalità di protezione da posta indesiderata nella catena di protezione da posta indesiderata in modo più aggressivo, è possibile ridurre la quantità di posta indesiderata. Di conseguenza, si risparmieranno risorse di elaborazione, larghezza di banda e di disco in modo da poter elaborare i messaggi più ambigui.

Infine, è necessario pianificare di monitorare l'efficacia generale delle funzionalità di protezione da posta indesiderata. Con un monitoraggio accurato, è possibile continuare a regolare le funzionalità di protezione da posta indesiderata per un corretto funzionamento nell'ambiente. Con questo approccio, all'avvio si consiglia di pianificare una configurazione non eccessivamente aggressiva delle funzionalità di protezione da posta indesiderata. Questo approccio consente di ridurre al minimo il numero di falsi positivi. Monitorando e regolando le funzionalità di protezione da posta indesiderata, è possibile incrementare l'aggressività relativa al tipo e agli attacchi di posta indesiderata subiti dall'organizzazione.

Inizio pagina

## Vedere anche


[Protezione di Office 365 posta indesiderata](https://support.office.com/en-us/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us)


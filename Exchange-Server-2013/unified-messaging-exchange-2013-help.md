---
title: " di messaggistica unificata: Exchange 2013 Help"
TOCTitle: " di messaggistica unificata"
ms:assetid: 004b5d1a-cae8-4034-ab65-db41bd2f7b97
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150478(v=EXCHG.150)
ms:contentKeyID: 50479892
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# di messaggistica unificata

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

Messaggistica unificata consente agli utenti di utilizzare il sistema di caselle vocali e altre funzionalità, incluse Outlook Voice Access e Regole ricezione chiamata. La messaggistica unificata combina la messaggistica vocale e di posta elettronica in una sola cassetta postale accessibile da diversi dispositivi. Gli utenti possono ascoltare i messaggi dalla Posta in arrivo o tramite Outlook Voice Access da qualsiasi telefono. È possibile controllare la modalità con cui gli utenti effettuano chiamate in uscita dalla messaggistica unificata e l'esperienza di chi effettua chiamate nell'organizzazione.

Oggi, gli amministratori IT gestiscono spesso il sistema di caselle vocali o le reti telefoniche e i sistemi di posta elettronica o le reti di dati come sistemi separati. Il sistema di caselle vocali e la posta elettronica sono caselle postali separate ospitate da server distinti e accessibili dal desktop per la posta elettronica e mediante telefono per la casella vocale.

Messaggistica unificata consente agli amministratori di Exchange di unire la messaggistica vocale e di posta elettronica in un'unica cassetta postale affinché i relativi utenti possano ascoltare i messaggi vocali nella propria cartella Posta in arrivo o utilizzando Outlook Voice Access da qualsiasi telefono. Utilizza l'archivio di Exchange per i messaggi di posta elettronica e vocali.

**Sommario**

New features

Unified Messaging features

Planning and deploying UM

Managing UM with the EAC and the Shell

Unified Messaging documentation

## Nuove funzionalità

La messaggistica unificata è stata introdotta dapprima in Microsoft Exchange Server 2007, ma era disponibile anche in Exchange 2010. L'impostazione della funzionalità di messaggistica unificata in Exchange 2013 è simile alle precedenti versioni di Exchange. Tuttavia, sono state aggiunte nuove funzionalità e sono state apportate modifiche all'architettura. La messaggistica unificata viene ora considerata un componente o funzionalità secondaria delle funzionalità vocali offerte in Exchange 2013. Il termine *messaggistica unificata* è ancora ampiamente utilizzato nei cmdlet di Exchange Management Shell e nei servizi associati alla messaggistica unificata e tutti i componenti di messaggistica unificata (inclusi dial plan, operatori automatici, criteri cassetta postale di messaggistica unificata e gateway IP di messaggistica unificata), insieme alla possibilità di gestire quei componenti di messaggistica unificata, si trovano all'interno del nodo Messaggistica unificata nel riquadro di navigazione dell'interfaccia di amministrazione di Exchange.

I seguenti argomenti forniscono un'introduzione in merito a informazioni sulle funzionalità nuove o potenziate presenti in Messaggistica unificata di Exchange 2013:

  - [Modifiche all'architettura VoIP](voice-architecture-changes-exchange-2013-help.md)

  - [Supporto IPv6 in messaggistica unificata](ipv6-support-in-unified-messaging-exchange-2013-help.md)

  - [Miglioramenti alla segreteria telefonica preview](voice-mail-preview-enhancements-exchange-2013-help.md)

  - [Aggiornamenti del cmdlet messaggistica unificati](unified-messaging-cmdlet-updates-exchange-2013-help.md)

Inizio pagina

## Funzionalità di messaggistica unificata

Le funzionalità del sistema di caselle vocali presenti in Messaggistica unificata offrono vantaggi sia per gli utenti finali sia per gli amministratori.

## Funzionalità per gli utenti finali

Quando si distribuisce la messaggistica unificata, gli utenti possono accedere al sistema di caselle vocali, alla posta elettronica e alle informazioni del calendario disponibili nella relativa cassetta postale da un client di posta elettronica, quale Outlook o MicrosoftOutlook Web App, da un telefono cellulare in cui è configurato MicrosoftExchange ActiveSync, quale un telefono Windows o da un telefono. Inoltre, gli utenti possono utilizzare le seguenti funzionalità:

  - **Accesso alle informazioni di Exchange   **Gli utenti abilitati alla messaggistica unificata possono accedere a una serie completa di funzionalità del sistema di caselle vocali dai telefoni cellulari abilitati per Internet, da MicrosoftOffice Outlook 2007 o versioni successive e da Outlook Web App. Queste funzionalità includono molte opzioni di configurazione del sistema di caselle vocali, la possibilità di riprodurre un messaggio vocale dal riquadro di lettura, utilizzando una versione integrata di Windows Media Player, o dall'elenco dei messaggi, utilizzando gli altoparlanti del computer.

  - **Ascolta al telefono**   La funzionalità Ascolta al telefono consente agli utenti abilitati alla messaggistica unificata di ascoltare i messaggi vocali al telefono. Se l'utente lavora in un ufficio aperto, sta utilizzando un computer pubblico o un computer non multimediale, o ancora sta ascoltando un messaggio vocale riservato, potrebbe non voler ascoltare il messaggio vocale con gli altoparlanti del computer. Egli può quindi ascoltare il messaggio vocale utilizzando qualsiasi telefono (di casa, dell'ufficio o cellulare).

  - **Modulo del sistema di caselle vocali**   Il modulo del sistema di caselle vocali è simile al modulo di posta elettronica predefinito. Offre agli utenti un'interfaccia per eseguire azioni quali la riproduzione, l'interruzione o la sospensione dei messaggi vocali, la riproduzione dei messaggi vocali da un telefono e l'aggiunta e la modifica di note.
    
    Il modulo del sistema di caselle vocali include Windows Media Player integrato e un campo per le note audio. Windows Media Player integrato e il campo delle note vengono visualizzati nel riquadro di lettura quando gli utenti visualizzano in anteprima un messaggio vocale oppure in una finestra separata quando il messaggio vocale viene aperto dagli utenti. Se gli utenti non sono abilitati alla messaggistica unificata o sul computer client non è stato installato un client di posta elettronica supportato, i messaggi vocali vengono visualizzati solo allegati di posta elettronica e il modulo del sistema di caselle vocali non è disponibile.

  - **Configurazione utente**   Un utente abilitato alla messaggistica unificata può configurare diverse opzioni del sistema di caselle vocali per la messaggistica unificata utilizzando Outlook Web App. Ad esempio, l'utente può configurare i numeri di accesso telefonico e il numero Ascolta al telefono del sistema di caselle vocali, nonché reimpostare il PIN di accesso ai messaggi vocali.

  - **Risponditore automatico   **Il risponditore automatico è in grado di rispondere a una chiamata in arrivo per conto dell'utente, riprodurre messaggi di saluto personali, registrare messaggi e inoltrare i messaggi registrati alla cartella Posta in arrivo come messaggi di posta elettronica.

  - **Regole ricezione chiamata**   Regole ricezione chiamata consente agli utenti abilitati al sistema di caselle vocali di stabilire la modalità di gestione dei risponditori automatici delle chiamate in ingresso. La modalità di applicazione delle regole ricezione chiamata alle chiamate in arrivo è simile alla modalità di applicazione delle regole di Posta in arrivo ai messaggi di posta elettronica in arrivo. Per impostazione predefinita, non è configurata alcuna regola risponditore automatico. Se un server Cassette postali risponde a una chiamata in arrivo, il chiamante è invitato a lasciare un messaggio vocale per l'utente chiamato. Utilizzando le regole ricezione chiamata, un chiamante può:
    
      - Lasciare un messaggio vocale per l'utente abilitato alla messaggistica unificata.
    
      - Eseguire il trasferimento a un contatto alternativo dell'utente abilitato alla messaggistica unificata.
    
      - Eseguire il trasferimento al sistema di caselle vocali di un contatto alternativo.
    
      - Eseguire il trasferimento ad altri numeri di telefono configurati dall'utente abilitato alla messaggistica unificata.
    
      - Utilizzare la funzionalità Trovami o individuare l'utente abilitato alla messaggistica unificata tramite un trasferimento da un operatore.

  - **Anteprima messaggio vocale**   Il server Cassette postali utilizza il riconoscimento vocale automatico (ASR) sui messaggi vocali appena creati. Quando gli utenti ricevono messaggi vocali, i messaggi contengono sia la registrazione sia il testo creati nel corso della registrazione. Gli utenti visualizzano il testo del messaggio vocale in un messaggio di posta elettronica da Outlook Web App o altri client di posta elettronica supportati.

  - **Messaggi in attesa di indicatore**   Indicatore di messaggio in attesa è una funzionalità disponibili in legacy più sistemi di segreteria telefonica e può fare riferimento a un meccanismo che indica l'esistenza di un nuovo messaggio. In Exchange 2007, questa funzionalità è stata fornita da un'applicazione di terze parti, indicato ricezione di un nuovo messaggio vocale da illuminazione luce al telefono da tavolo. Questa funzionalità è stato aggiunto al Exchange 2010 e software di terze parti non è più necessaria. Abilitazione o disabilitazione dell'indicatore di messaggio in attesa viene eseguita nella cassetta postale dell'utente o in un criterio cassetta postale di messaggistica UNIFICATA.

  - **Notifiche di chiamate senza risposta e messaggi vocali tramite SMS**   Se gli utenti sono membri di un'implementazione ibrida o di Office 365 e configurano il numero del proprio cellulare nelle impostazioni del sistema di caselle vocali e impostano l'inoltro delle chiamate, possono ricevere notifiche sulle chiamate senza risposta e sui nuovi messaggi vocali direttamente sui loro telefoni cellulari, sotto forma di messaggi di testo tramite il servizio SMS. Tuttavia, per ricevere questo tipo di notifiche, gli utenti devono prima configurare la messaggistica di testo e abilitare le notifiche per l'account.

  - **Sistema di caselle vocali protette**   Il sistema di caselle vocali protette è una funzionalità di messaggistica unificata che consente agli utenti di inviare messaggi di posta privati. Il messaggio di posta è protetto dal servizio AD RMS (Active Directory Rights Management Services) e gli utenti non possono eseguire l'inoltro, la copia o l'estrazione del file vocale dal messaggio di posta elettronica. Sistema di caselle vocali protette aumenta la riservatezza della messaggistica unificata e consente agli utenti di limitare il pubblico per i messaggi vocali. Tale funzionalità è simile alla modalità di gestione dei messaggi di posta elettronica privati in Exchange 2007, ma viene ora applicata anche ai messaggi vocali.

  - **Outlook Voice Access   **Sono disponibili due interfacce utente di messaggistica unificata agli utenti abilitati alla messaggistica unificata: l'interfaccia utente telefonica (TUI) e l'interfaccia utente vocale (VUI). L'insieme di queste due interfacce viene definito Outlook Voice Access. Gli utenti di Outlook Voice Access possono utilizzare Outlook Voice Access quando accedono al sistema di caselle vocali da un telefono interno o esterno. Gli utenti abilitati alla messaggistica unificata che effettuano una chiamata al sistema di caselle vocali possono accedere alla propria cassetta postale utilizzando Outlook Voice Access. Utilizzando un telefono, un utente abilitato alla messaggistica unificata può:
    
      - Accedere al sistema di caselle vocali
    
      - Ascoltare, inoltrare o rispondere ai messaggi di posta elettronica
    
      - Ascoltare le informazioni del calendario
    
      - Accedere o chiamare contatti memorizzati nella directory dell'organizzazione o un singolo contatto o gruppo di contatti presenti tra i contatti personali.
    
      - Accettare o annullare le convocazioni di riunione
    
      - Impostare un messaggio vocale per consentire ai chiamanti di sapere che l'utente chiamato non è disponibile
    
      - Impostare preferenze di protezione dell'utente e opzioni personali

  - **Indirizzamento di gruppo con Outlook Voice Access**   In Exchange 2007, gli utenti potevano utilizzare l'interfaccia telefonica o l'interfaccia vocale in Outlook Voice Access per inviare messaggi di posta elettronica e vocali una volta eseguito l'accesso alla cassetta postale. Tuttavia, gli utenti potevano solo inviare un unico messaggio di posta elettronica a un singolo utente dei Contatti personali e a più destinatari dalla directory aggiungendo ogni destinatario singolarmente o aggiungendo il nome di una lista di distribuzione dalla directory dell'organizzazione. In Exchange 2013, gli utenti che accedono alla propria cassetta postale utilizzando Outlook Voice Access possono inviare messaggi di posta elettronica e vocali anche agli utenti di un gruppo salvato nei Contatti personali.

Inizio pagina

## Funzionalità amministrative

Attualmente, la maggior parte degli utenti e dei reparti IT gestisce il sistema di caselle vocali separatamente dalla posta elettronica. Il sistema di caselle vocali e la posta elettronica sono caselle postali separate ospitate da server distinti e accessibili dal desktop per la posta elettronica e mediante telefono per il sistema di caselle vocali. La Messaggistica unificata offre un archivio integrato per tutti i messaggi e l'accesso al contenuto attraverso computer e telefono.

Gli amministratori di Exchange possono gestire la messaggistica unificata utilizzando la stessa interfaccia utilizzata per gestire il resto di Exchange, utilizzando l'interfaccia di amministrazione di Exchange ed Exchange Management Shell. Possono:

  - Gestire il sistema di caselle vocali e la posta elettronica da una singola piattaforma

  - Gestire la messaggistica unificata mediante comandi di script

  - Creare infrastrutture di messaggistica unificata altamente disponibili e affidabili

La Messaggistica unificata di Exchange 2013 offre agli amministratori:

  - **Un sistema di caselle vocali completo**   Messaggistica unificata offre una soluzione di caselle vocali completa utilizzando un'unica infrastruttura di archiviazione, trasporto e directory. L'archiviazione viene fornita da un server Cassette postali e l'inoltro delle chiamate in arrivo da un gateway VoIP o IP PBX è gestito da un server Accesso client. Tutti i messaggi di posta elettronica e vocali possono essere gestiti da un singolo punto di gestione, utilizzando una singola interfaccia di amministrazione e un insieme di strumenti.

  - **Un modello di protezione Exchange   **Il servizio di messaggistica unificata di MicrosoftExchange su un server Cassette postali e il servizio di routing delle chiamate di messaggistica unificata di MicrosoftExchange su un server Accesso client funzionano come un singolo account del server Exchange.

  - **Consolidamento dei sistemi di caselle vocali**   Al momento, la maggior parte dei sistemi di messaggistica vocale richiedono che tutti i componenti di messaggistica vocale siano installati in ogni postazione fisica dell'ufficio dell'organizzazione. Con questo tipo di disposizione, i sistemi di caselle vocali nelle succursali si trovano all'esterno dell'ufficio centrale e devono essere amministrati in sede. Spesso il risultato corrisponde a maggiori oneri e complessità a livello di amministrazione. Messaggistica unificata consente di gestire il proprio sistema di caselle vocali da una postazione centrale. Per creare un sistema di gestione centralizzato per la messaggistica unificata, è possibile posizionare alcuni dei server Exchange in un datacenter o altre posizioni e il resto dei server Exchange sul posto e, quindi, distribuire i gateway VoIP, IP PBX o session border controller in tutte le succursali per sostituire il sistema di messaggistica vocale per ciascuna succursale. La distribuzione di un sistema di messaggistica vocale centralizzato di questo tipo può determinare un significativo risparmio a livello di costi legati all'hardware e all'amministrazione.

  - **Ruoli amministrativi di messaggistica unificata integrati**   L'insieme di ruoli amministrativi specifici della messaggistica unificata per la gestione delle funzionalità di messaggistica unificata e del sistema di caselle vocali include quanto riportato di seguito:
    
      - Cassette postali di messaggistica unificata
    
      - Prompt di messaggistica unificata
    
      - Messaggistica unificata

  - **Supporto fax in ingresso**   Exchange 2013 offre un supporto relativo ai fax in ingresso per gli utenti in possesso di una cassetta postale abilitata alla messaggistica unificata. Possono ricevere messaggi fax tramite chiamate effettuate al loro numero di interno.
    
    I clienti che richiedono una soluzione fax saranno necessario distribuire una soluzione di partner fax. Soluzioni partner fax sono rese disponibili da diversi partner fax. Le soluzioni partner fax sono progettate per essere strettamente integrato con Exchange e consentire agli utenti abilitati alla messaggistica UNIFICATA di ricevere messaggi fax in arrivo. È possibile trovare una soluzione di partner fax visitando [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238).

  - **Supporto per più lingue**   Tutti i language pack disponibili includono il motore di sintesi vocale (TTS) e le richieste preregistrate per una lingua specificata e il supporto di ASR. Tuttavia, alcuni language pack è supportato da Anteprima messaggio vocale. Il language pack inglese USA (en-US) è incluso nel supporto di installazione e ulteriori language pack di messaggistica UNIFICATA può essere scaricato dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542).

  - **Operatore automatico**   Un operatore automatico è un insieme di prompt vocali che consente agli utenti esterni o interni di accedere al sistema di caselle vocali. Gli utenti possono utilizzare il tastierino numerico del telefono o gli input vocali per spostarsi nella struttura del menu dell'operatore automatico, chiamare un utente o individuare un utente all'interno dell'organizzazione e quindi eseguire la chiamata. Un operatore automatico consente all'amministratore di:
    
      - Creare un menu personalizzato per gli utenti esterni.
    
      - Definire messaggi di saluto informativi, messaggi di saluto per gli orari di ufficio e non di ufficio.
    
      - Definire la pianificazione delle festività.
    
      - Descrivere come eseguire la ricerca nella directory dell'organizzazione.
    
      - Descrivere la modalità di connessione al numero di interno di un utente, in modo da consentire agli utenti esterni di chiamare gli utenti specificandone l'interno.
    
      - Descrivere la modalità di esecuzione della ricerca nella directory dell'organizzazione, in modo da consentire ai chiamanti esterni di effettuare tale ricerca e chiamare un utente specifico.
    
      - Abilitare gli utenti esterni alle chiamate verso l'operatore.

Inizio pagina

## Pianificazione e distribuzione della messaggistica unificata

La messaggistica unificata richiede l'integrazione della distribuzione di Exchange Server nel sistema di telefonia esistente all'interno dell'organizzazione. Una distribuzione corretta richiede un'attenta analisi dell'infrastruttura telefonica esistente e l'esecuzione della procedura di pianificazione corretta per distribuire e gestire il sistema di caselle vocali in Messaggistica unificata.

Quando si pianifica la distribuzione della messaggistica unificata, è necessario prendere in considerazione la progettazione ed altre questioni che potrebbero influire sulla possibilità di raggiungere gli obiettivi dell'organizzazione in caso di distribuzione della messaggistica unificata. In genere, più la topologia della messaggistica unificata è semplice, più saranno semplici la distribuzione e la manutenzione. Installare una quantità di server Accesso client e Cassette postali e creare una quantità di componenti di messaggistica unificata corrispondenti al numero di dial plan di messaggistica unificata, operatori automatici e criteri cassetta postale di messaggistica unificata necessari per supportare gli obiettivi aziendali e organizzativi. Le grandi aziende con ambienti di rete e di telefonia complessi, più unità aziendali o altre strutture complesse richiedono una maggiore pianificazione rispetto alle organizzazioni più piccole, le quali presentano esigenze di messaggistica unificata relativamente semplici.

Per una corretta distribuzione della messaggistica unificata, è necessario considerare e valutare diversi fattori. È necessario comprendere i diversi aspetti della messaggistica unificata, nonché ogni componente e funzione, in modo tale da poter pianificare nel modo adeguato l'infrastruttura della messaggistica unificata e la relativa distribuzione. Destinare del tempo alla pianificazione e allo studio di questi fattori consente di evitare eventuali problemi durante la distribuzione della messaggistica unificata all'interno dell'organizzazione:

  - Le esigenze dell'organizzazione.

  - I requisiti di protezione dell'organizzazione.

  - La telefonia esistente, la rete a commutazione di circuito e il sistema di caselle vocali corrente.

  - La struttura della rete IP a commutazione di pacchetto corrente. Ciò include i propri dispositivi e punti di connessione LAN e WAN.

  - L'ambiente Active Directory corrente.

  - Il numero di utenti che dovrà essere supportato.

  - Il numero di server Accesso client e Cassette postali necessari.

  - Se verrà effettuata un'integrazione della messaggistica unificata con Microsoft Lync Server per l'abilitazione di Enterprise Voice.

  - Il posizionamento di gateway VoIP, apparecchiature telefoniche e server Accesso client e Cassette postali.

  - Il tipo di distribuzione della messaggistica unificata: locale o ibrido.

  - I requisiti di archiviazione per gli utenti del sistema di caselle vocali.

Inizio pagina

## Gestione della messaggistica unificata tramite Interfaccia di amministrazione di Exchange e Shell

**Gestione tramite Interfaccia di amministrazione di Exchange**

Exchange 2013 offre una singola console di gestione unificata per l'organizzazione che include tutti i componenti e le funzionalità di messaggistica unificata. L'interfaccia di amministrazione di Exchange offre un'interfaccia semplificata e ottimizzata per la gestione delle distribuzioni in locale, online o ibride. L'interfaccia di amministrazione di Exchange in Exchange 2013 sostituisce Exchange Management Console (EMC) e il Pannello di controllo di Exchange (ECP) in Exchange 2010. Alcune delle funzionalità dell'interfaccia di amministrazione di Exchange comprendono:

  - **Visualizzazione elenco**   La visualizzazione elenco in Interfaccia di amministrazione di Exchange è stata progettata per rimuovere le limitazioni presenti nel Pannello di controllo di Exchange. ECP limitava la visualizzazione a 500 oggetti e, se si desiderava visualizzare gli oggetti non riportati nel riquadro dei dettagli, si doveva ricorrere alla ricerca e al filtraggio per trovare quegli oggetti specifici. In Exchange 2013, il limite visualizzabile nell'elenco EAC è di circa 20.000 oggetti. Inoltre, è stato aggiunto il paging per poter sfogliare i risultati. È anche possibile configurare le dimensioni delle pagine ed effettuare l'esportazione in un file CSV.

  - **Aggiunta/rimozione di colonne dalla visualizzazione elenco Destinatario**   È possibile scegliere quali colonne visualizzare e salvare visualizzazioni elenco personalizzate.

  - **Protezione della directory virtuale di ECP**   È possibile eseguire una partizione dell'accesso da Internet e Intranet dall'interno della directory virtuale IIS del Pannello di controllo di Exchange per consentire o meno le funzionalità di gestione. Con questa funzionalità, è possibile concedere o negare l'accesso agli utenti che tentano di accedere al Pannello di controllo di Exchange utilizzando un accesso Internet esterno al proprio ambiente organizzativo, consentendo, però, l'accesso alle opzioni di Outlook Web App di un utente finale.

  - **Gestione di cartelle pubbliche**   In Exchange 2010 e Exchange 2007, le cartelle pubbliche erano gestite tramite la console di amministrazione delle cartelle pubbliche. Le cartelle pubbliche ora sono in Interfaccia di amministrazione di Exchange e non serve uno strumento a parte per gestirle.

  - **Notifiche**   In Exchange 2013, l'interfaccia di amministrazione di Exchange ora comprende un visualizzatore di notifiche per visualizzare lo stato dei processi di lunga durata e, se lo si desidera, è possibile ricevere la notifica con un messaggio di posta elettronica al completamento del processo.

  - **Editor utenti Controllo di accesso basato sui ruoli (RBAC)**   In Exchange 2010, era possibile utilizzare l'editor utenti RBAC per aggiungere utenti ai gruppi di ruoli di gestione. In Exchange 2013, la funzionalità Editor utente RBAC è ora disponibile nell'Interfaccia di amministrazione di Exchange e non è richiesto un ulteriore strumento per la gestione di RBAC.

  - **Strumenti di messaggistica unificata**   In Exchange 2010, era possibile utilizzare gli strumenti Statistiche delle chiamate e Registri chiamate utente per ottenere facilmente statistiche di messaggistica unificata e informazioni su chiamate specifiche per un utente abilitato alla messaggistica unificata. In Exchange 2013, gli strumenti Statistiche delle chiamate e Registri chiamate utente sono ora disponibili nell'Interfaccia di amministrazione di Exchange e non sono richiesti altri strumenti per gestirli.

**Gestione di Shell**

Exchange Management Shell, incorporata nella tecnologia Windows PowerShell, è una potente interfaccia della riga di comando che consente l'automazione delle attività amministrative. Shell consente di gestire ogni aspetto di Exchange. È possibile abilitare nuovi account di posta elettronica, creare connettori di invio e ricezione, configurare le proprietà di un database, gestire tutti gli aspetti della messaggistica unificata e altro ancora. Shell è in grado di eseguire tutte le attività eseguibili dall'interfaccia di amministrazione di Exchange più altre attività che non possono essere svolte nella suddetta interfaccia. In realtà, qualsiasi operazione si esegue dall'interfaccia di amministrazione di Exchange, è lo Shell che svolge l'attività in background.

Inizio pagina

## Documentazione di messaggistica unificata

Nella seguente tabella, sono riportati i collegamenti agli argomenti che offrono maggiori informazioni sulla messaggistica unificata di Exchange e ne facilitano la gestione.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Argomento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="new-voice-mail-features-exchange-2013-help.md">Nuove funzionalità di posta vocale</a></p></td>
<td><p>Ulteriori informazioni sulle nuove funzionalità di Microsoft Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Pianificazione per la messaggistica unificata</a></p></td>
<td><p>Maggiori informazioni sui concetti e le informazioni necessari per la pianificazione di una distribuzione di messaggistica unificata.</p></td>
</tr>
<tr class="odd">
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Distribuzione di segreteria telefonica e messaggistica UNIFICATA</a></p></td>
<td><p>Maggiori informazioni sui requisiti e i passaggi coinvolti nella distribuzione del sistema di caselle vocali e della messaggistica unificata.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-languages-prompts-and-greetings-exchange-2013-help.md">Messaggi di saluto, istruzioni e lingue di messaggistica UNIFICATA</a></p></td>
<td><p>Ulteriori informazioni sui Language Pack di messaggistica unificata e sulle impostazioni per la lingua.</p></td>
</tr>
<tr class="odd">
<td><p><a href="telephone-system-integration-with-um-exchange-2013-help.md">Integrazione del telefono sistema con la messaggistica UNIFICATA</a></p></td>
<td><p>Informazioni sull'integrazione della rete di telefonia con la funzionalità di messaggistica unificata.</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md">Connettere il sistema di segreteria telefonica alla rete telefonica</a></p></td>
<td><p>Maggiori informazioni su come utilizzare e configurare i componenti di messaggistica unificata per collegare la rete telefonica alla messaggistica unificata di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="automatically-answer-and-route-incoming-calls-exchange-2013-help.md">Rispondere automaticamente e il routing delle chiamate in arrivo</a></p></td>
<td><p>Maggiori informazioni su come creare operatori automatici di messaggistica unificata e gestire le impostazioni per i menu di navigazione, i messaggi di saluto e gli orari di ufficio e non di ufficio.</p></td>
</tr>
<tr class="even">
<td><p><a href="set-up-voice-mail-for-users-exchange-2013-help.md">Configurazione di segreteria telefonica per gli utenti</a></p></td>
<td><p>Ulteriori informazioni su come creare e gestire cassette postali di messaggistica unificata e su come abilitare la funzionalità di messaggistica unificata per gli utenti.</p></td>
</tr>
<tr class="odd">
<td><p><a href="set-up-client-voice-mail-features-exchange-2013-help.md">Installazione delle funzionalità di posta vocale del client</a></p></td>
<td><p>Ulteriori informazioni su come configurare le funzionalità del client affinché gli utenti possano accedere e gestire i propri messaggi vocali.</p></td>
</tr>
<tr class="even">
<td><p><a href="set-outlook-voice-access-pin-security-exchange-2013-help.md">Configurare la protezione di Outlook Voice Access PIN</a></p></td>
<td><p>Ulteriori informazioni su come impostare i requisiti di PIN per gli utenti di Outlook Voice Access.</p></td>
</tr>
<tr class="odd">
<td><p><a href="protect-voice-mail-exchange-2013-help.md">Sistema di caselle vocali protette</a></p></td>
<td><p>Ulteriori informazioni su come utilizzare la messaggistica unificata per proteggere i messaggi vocali.</p></td>
</tr>
<tr class="even">
<td><p><a href="run-reports-for-voice-mail-calls-exchange-2013-help.md">Eseguire report per le chiamate di posta vocale</a></p></td>
<td><p>Ulteriori informazioni sui rapporti di chiamata per la messaggistica unificata.</p></td>
</tr>
</tbody>
</table>


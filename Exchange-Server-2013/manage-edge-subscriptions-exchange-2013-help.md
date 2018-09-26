---
title: 'Gestione delle sottoscrizioni Edge: Exchange 2013 Help'
TOCTitle: Gestione delle sottoscrizioni Edge
ms:assetid: 27de4104-fb8e-4eab-9ad2-a64f81a4fb69
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996865(v=EXCHG.150)
ms:contentKeyID: 61183402
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione delle sottoscrizioni Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2018-04-16_

In questo argomento vengono fornite informazioni dettagliate su un'ampia gamma di attività di gestione della sottoscrizione Edge.

**Sommario**

Subscribe an Edge Transport server

Remove an Edge subscription

Resubscribe an Edge Transport Server

Add or remove a Mailbox Server

Run EdgeSync manually

Verify EdgeSync results

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "EdgeSync" e "server Trasporto Edge" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È necessario avere un server Edge sottoscritto nel sito Active Directory con connessione a Internet. Per ulteriori informazioni, vedere [Configurazione del flusso della posta Internet tramite un server Trasporto Edge sottoscritto](configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Sottoscrivere un server Trasporto Edge

Uno o più server Trasporto Edge possono essere sottoscritti in un solo sito di Active Directory. Se nella rete perimetrale vengono distribuiti server Trasporto Edge aggiuntivi e vengono sottoscritti allo stesso sito di Active Directory in cui è già presente una sottoscrizione Edge, si verificano le seguenti azioni:

  - Viene creato un nuovo oggetto sottoscrizione Edge in Active Directory.

  - Vengono creati account ESRA aggiuntivi per ogni server Cassette postali nel sito di Active Directory. Questi account vengono replicati in AD LDS e utilizzati dal processo di sincronizzazione EdgeSync durante la sincronizzazione con il nuovo server.

  - La nuova sottoscrizione Edge viene aggiunta all'elenco dei server di origine del connettore di invio automatico su Internet. Il carico legato all'elaborazione dei messaggi inviati a quel connettore verrà bilanciato tra i server Trasporto Edge sottoscritti.

  - Viene creato automaticamente un connettore di invio dei messaggi in ingresso dal server Trasporto Edge all'organizzazione di Exchange.

  - Viene avviata la sincronizzazione EdgeSync con il server Trasporto Edge.

## Eliminazione di una sottoscrizione Edge

È possibile rimuovere la sottoscrizione Edge dall'organizzazione di Exchange o dall'organizzazione di Exchange e dal server Trasporto Edge. Se si pensa di sottoscrivere di nuovo in un secondo momento un server Trasporto Edge nell'organizzazione di Exchange, non rimuovere la sottoscrizione Edge dal server Trasporto Edge. Quando si rimuove la sottoscrizione Edge dal server Trasporto Edge, tutti i dati replicati vengono eliminati da AD LDS. Se sono presenti diversi dati del destinatario, potrebbe essere necessario parecchio tempo.

Per rimuovere completamente una sottoscrizione Edge, è necessario eseguire questa procedura nel server Trasporto Edge da rimuovere e in un server Cassette postali di Exchange 2013 nel sito di Active Directory dove è sottoscritto il server Trasporto Edge.

Dopo aver rimosso la sottoscrizione Edge, la sincronizzazione delle informazioni di AD LDS si interrompe. Tutti gli account archiviati in ADAM vengono rimossi e il server Trasporto Edge viene rimosso dall'elenco dei server di origine di tutti i connettori di invio. Non sarà più possibile utilizzare le funzionalità del server Trasporto Edge che si basano sui dati di Active Directory.

1.  Per rimuovere la sottoscrizione Edge dal server Trasporto Edge, utilizzare la seguente sintassi.
    
    ```powershell
      Remove-EdgeSubscription <EdgeTransportServerIdentity>
    ```
    
    Ad esempio, per rimuovere la sottoscrizione Edge nel server Trasporto Edge di nome Edge01, eseguire il seguente comando.
    
    ```powershell
      Remove-EdgeSubscription Edge01
    ```

2.  Per rimuovere la sottoscrizione Edge dal server Cassette postali, utilizzare la seguente sintassi.
    
    ```powershell
      Remove-EdgeSubscription <MailboxServerIdentity>
    ```
    
    Ad esempio, per rimuovere la sottoscrizione Edge nel server Cassette postali di nome Mailbox01, eseguire il seguente comando.
    
    ```powershell
      Remove-EdgeSubscription Mailbox01
    ```

È necessario rimuovere la sottoscrizione Edge se:

  - Si desidera che il server Trasporto Edge non sia più incluso nel processo di sincronizzazione EdgeSync. Sarà necessario rimuovere la sottoscrizione Edge sia dal server Trasporto Edge che dall'organizzazione di Exchange.

  - Un server Trasporto Edge viene privato dell'autorizzazione. In questo scenario, sarà solo necessario rimuovere la sottoscrizione Edge dall'organizzazione di Exchange. Se il ruolo del server Trasporto Edge viene disinstallato da un computer, verranno rimossi anche l'istanza AD LDS e tutti i dati di Active Directory archiviati in AD LDS.

  - Si vuole modificare l'associazione del sito di Active Directory per la sottoscrizione Edge. Sarà solo necessario rimuovere la sottoscrizione Edge dall'organizzazione di Exchange. Dopo questa operazione, sarà possibile sottoscrivere nuovamente il server Trasporto Edge a un sito diverso di Active Directory.

Quando si rimuove una sottoscrizione Edge dall'organizzazione di Exchange:

  - Viene interrotta la sincronizzazione delle informazioni da Active Directory ad AD LDS.

  - Gli account ESRA vengono rimossi sia da Active Directory che da AD LDS.

  - Il server Trasporto Edge viene rimosso dalla proprietà *SourceTransportServers* di qualsiasi connettore di invio.

  - Il connettore di invio automatico dei messaggi in ingresso dal server Trasporto Edge all'organizzazione di Exchange viene rimosso da AD LDS.

Quando si rimuove la sottoscrizione Edge da un server Trasporto Edge:

  - Non è più possibile utilizzare le funzionalità del server Trasporto Edge che si basano sui dati di Active Directory.

  - I dati replicati vengono rimossi da AD LDS.

  - Le attività che erano state disabilitate alla creazione della sottoscrizione Edge vengono riabilitate per consentire la configurazione locale.

## Nuova sottoscrizione di un server Trasporto Edge

Talvolta, potrebbe essere necessario risottoscrivere un server Trasporto Edge in un sito di Active Directory. Quando viene ricreata la sottoscrizione Edge, vengono generate nuove credenziali ed è necessario eseguire il processo completo di sottoscrizione Edge. È necessario risottoscrivere un server Trasporto Edge se:

  - Si aggiungono nuovi server Cassette postali nel sito di Active Directory sottoscritto e si vuole che il nuovo server Cassette postali partecipi alla sincronizzazione di EdgeSync.

  - Il codice di licenza del server Trasporto Edge è stato applicato dopo aver creato la sottoscrizione Edge. Le informazioni sulle licenze per il server Trasporto Edge vengono acquisite quando viene creata la sottoscrizione Edge. Per visualizzare i server Trasporto Edge come sottoscritti, è necessario sottoscriverli nell'organizzazione di Exchange dopo che il codice di licenza è stato applicato al server Trasporto Edge. Se il codice di licenza viene applicato nel server Trasporto Edge dopo l'esecuzione del processo di sottoscrizione Edge, le informazioni sulla licenza non verranno aggiornate nell'organizzazione di Exchange. Sarà quindi necessario sottoscrivere nuovamente il server Trasporto Edge.

  - Le credenziali dell'account ESRA sono state compromesse.
    

    > [!IMPORTANT]
    > Per sottoscrivere nuovamente un server Trasporto Edge, esportare un nuovo file sottoscrizione Edge nel server Trasporto Edge, quindi importare il file XML in un server Cassette postali. È necessario sottoscrivere nuovamente il server Trasporto Edge nello stesso sito di Active&nbsp;Directory a cui era stato sottoscritto originariamente. Non è necessario prima rimuovere la sottoscrizione di Edge originaria.&nbsp;Il processo di risottoscrizione sovrascriverà la sottoscrizione Edge esistente.



## Aggiungere o rimuovere un server Cassette postali

Se si aggiunge un server Cassette postali a un sito di Active Directory in cui è già sottoscritto un server Trasporto Edge, il nuovo server Cassette postali non partecipa automaticamente alla sincronizzazione di EdgeSync. Per far sì che un nuovo server Cassette postali partecipi alla sincronizzazione di EdgeSync, è necessario sottoscrivere di nuovo ogni server Trasporto Edge nel sito di Active Directory.

La rimozione di un server Cassette postali da un sito di Active Directory a cui è sottoscritto un server Trasporto Edge non inciderà sulla sincronizzazione EdgeSync, a meno che il server Cassette postali eliminato non sia l'unico del sito. Se vengono rimossi tutti i server Cassette postali dal sito di Active Directory a cui è sottoscritto un server Trasporto Edge, i server Trasporto Edge sottoscritti del sito verranno isolati.

## Eseguire manualmente EdgeSync

Si potrebbe voler eseguire EdgeSync manualmente se sono state apportate modifiche significative alla configurazione o ai destinatari in Active Directory e se si vuole che le modifiche vengano sincronizzate immediatamente. È possibile eseguire una sincronizzazione completa o sincronizzare solo le modifiche apportate dall'ultima replica.

Una sincronizzazione EdgeSync manuale reimposta la pianificazione della sincronizzazione EdgeSync. La successiva sincronizzazione automatica si basa su quando è stata eseguita la sincronizzazione manuale.

Per eseguire manualmente EdgeSync, utilizzare la seguente sintassi.
```powershell
    Start-EdgeSynchronization [-Server <MailboxServerIdentity>] [-TargetServer <EdgeTransportServerIdentity> [-ForceFullSync]
```

Nell'esempio riportato di seguito viene avviata la sincronizzazione EdgeSync con le seguenti opzioni:

  - La sincronizzazione viene avviata dal server Cassette postali di Exchange 2013 denominato Mailbox01.

  - Vengono sincronizzati tutti i server Trasporto Edge.

  - Vengono sincronizzate solo le modifiche apportate dall'ultima replica.

<!-- end list -->

```powershell
Start-EdgeSynchronization -Server Mailbox01
```

In questo esempio viene avviata la sincronizzazione EdgeSync con le opzioni seguenti:

  - La sincronizzazione viene avviata dal server Cassette postali locali.

  - Viene sincronizzato solo il server Trasporto Edge Edge03.

  - Tutti i dati di configurazione e del destinatario vengono sincronizzati completamente.

<!-- end list -->

```powershell
Start-EdgeSynchronization -TargetServer Edge03 -ForceFullSync
```

## Verifica dei risultati di EdgeSync

È possibile utilizzare il cmdlet **Test-EdgeSynchronization** per verificare che la sincronizzazione Edge funzioni correttamente. Questo cmdlet segnala lo stato di sincronizzazione dei server Trasporto Edge sottoscritti.

L'output di questo cmdlet consente di visualizzare gli oggetti non sincronizzati con il server Trasporto Edge. L'attività confronta i dati memorizzati in Active Directory con i dati memorizzati in AD LDS e segnala eventuali incoerenze dei dati.

È possibile utilizzare il parametro *ExcludeRecipientTest* nel cmdlet **Test-EdgeSynchronization** per escludere dalla convalida la sincronizzazione dei dati del destinatario. Se si include questo parametro, viene convalidata solo la sincronizzazione degli oggetti di configurazione. La convalida dei dati del destinatario richiede tempi più lunghi della convalida solo dei dati di configurazione.

## Verifica dei risultati di EdgeSync relativi a un solo destinatario

Per verificare i risultati di EdgeSync relativi a un solo destinatario, utilizzare la seguente sintassi in un server Cassette postali nel sito di Active Directory sottoscritto.

```powershell
Test-EdgeSynchronization -VerifyRecipient <emailaddress>
```

Questo esempio verifica i risultati di EdgeSync per l'utente kate@contoso.com.

```powershell
Test-EdgeSynchronization -VerifyRecipient kate@contoso.com
```

Inizio pagina


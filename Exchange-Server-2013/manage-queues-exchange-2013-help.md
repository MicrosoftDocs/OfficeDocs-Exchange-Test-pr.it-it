---
title: 'Gestire le code: Exchange 2013 Help'
TOCTitle: Gestire le code
ms:assetid: 37f11378-a884-4aff-ab55-689f40a46321
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997263(v=EXCHG.150)
ms:contentKeyID: 51407352
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire le code

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-01-31_

In Microsoft Exchange Server 2013, è possibile utilizzare il Visualizzatore code nella Casella degli strumenti di Exchange o di Exchange Management Shell per gestire le code. Per ulteriori informazioni sull'utilizzo dei cmdlet per la gestione delle code in Exchange Management Shell, vedere [Utilizzare Exchange Management Shell per gestire le code](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Code" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Visualizzazione delle code

## Utilizzare il Visualizzatore code nella Casella degli strumenti di Exchange per visualizzare le code

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange 2013** \> **Casella degli strumenti di Exchange**.

2.  Nella sezione **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code** per aprire lo strumento in una nuova finestra.

3.  In Visualizzatore code, fare clic sulla scheda **Code**. Viene visualizzato un elenco di tutte le code presenti nel server a cui si è connessi.

4.  È possibile utilizzare il collegamento **Esporta elenco** nel riquadro azioni per esportare l'elenco di code. Per ulteriori informazioni, vedere [Esportare elenchi dal Visualizzatore code](export-lists-from-queue-viewer-exchange-2013-help.md).

## Visualizzazione delle code tramite Shell

Per visualizzare le code, utilizzare la sintassi seguente.
```powershell
    Get-Queue [-Filter <Filter> -Server <ServerIdentity> -Include <Internal | External | Empty | DeliveryType> -Exclude <Internal | External | Empty | DeliveryType>]
```
In questo esempio vengono visualizzate le informazioni di base sulle code non vuote del server Cassette postali di Exchange 2013 denominato Mailbox01.

```powershell
Get-Queue -Server Mailbox01 -Exclude Empty
```

In questo esempio vengono visualizzate informazioni dettagliate su tutte le code contenenti più di 100 messaggi sul server Cassette postali su cui viene eseguito il comando.

```powershell
Get-Queue -Filter {MessageCount -gt 100} | Format-List
```

## Utilizzare Shell per visualizzare un riepilogo di informazioni sulle code su più server Exchange

Il cmdlet **Get-QueueDigest** fornisce una visualizzazione aggregata di alto livello dello stato delle code su tutti i server in uno specifico ambito, ad esempio un gruppo di disponibilità del database, un sito Active Directory, un elenco di server o l'intera foresta Active Directory. Tenere presente che le code in un server Trasporto Edge sottoscritto nella rete perimetrale non sono incluse nei risultati. Inoltre, **Get-QueueDigest** è disponibile in un server Trasporto Edge, ma i risultati sono limitati alle code nel server Trasporto Edge.


> [!NOTE]
> Per impostazione predefinita, il cmdlet <STRONG>Get-QueueDigest</STRONG> visualizza le code di recapito contenenti dieci o più messaggi. I risultati restituiti risalgono da uno a due minuti prima. Per istruzioni su come modificare i valori predefiniti, vedere <A href="configure-get-queuedigest-exchange-2013-help.md">Configurazione di Get-QueueDigest</A>.



Per visualizzare le informazioni di riepilogo sulle code su più server Exchange, eseguire il comando seguente:
```powershell
    Get-QueueDigest <-Server <ServerIdentity1,ServerIdentity2,..> | -Dag <DagIdentity1,DagIdentity2...> | -Site <ADSiteIdentity1,ADSiteIdentity2...> | -Forest> [-Filter <Filter>]
```
In questo esempio viene visualizzato il riepilogo delle informazioni sulle code su tutti i server Cassette postali di Exchange 2013 sul sito di Active Directory denominato FirstSite, dove il numero dei messaggi è superiore a 100.

```powershell
Get-QueueDigest -Site FirstSite -Filter {MessageCount -gt 100}
```

In questo esempio viene visualizzato il riepilogo delle informazioni sulle code su tutti i server Cassette postali di Exchange 2013 del gruppo di disponibilità del database (DAG, database availability group) denominato DAG01, dove lo stato delle code ha il valore **Retry**.

```powershell
Get-QueueDigest -Dag DAG01 -Filter {Status -eq "Retry"}
```

## Ripresa delle code

Riprendendo una coda, si riavviano le attività in uscita in una coda il cui stato è Sospeso. Per poter rendere efficace questa azione, lo stato della coda deve essere Sospeso. Quando si riprende una coda, lo stato dei messaggi nella coda non cambia. I messaggi con lo stato Sospeso restano sospesi e non lasciano la coda.

## Utilizzare il Visualizzatore code nella Casella degli strumenti di Exchange per riprendere le code

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange 2013** \> **Casella degli strumenti di Exchange**.

2.  Nella sezione **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code** per aprire lo strumento in una nuova finestra.

3.  In Visualizzatore code, fare clic sulla scheda **Code**. Viene visualizzato un elenco di tutte le code presenti nel server a cui si è connessi.

4.  Fare clic su **Crea filtro** e immettere l'espressione del filtro nel modo seguente:
    
    1.  Selezionare **Stato** dall'elenco a discesa delle proprietà della coda.
    
    2.  Selezionare **Uguale a** dall'elenco a discesa degli operatori di confronto.
    
    3.  Selezionare **Sospeso** dall'elenco a discesa dei valori.

5.  Scegliere **Applica filtro**. Vengono visualizzate tutte le code sul server al momento sospese.

6.  Selezionare una o più code dall'elenco, fare clic con il pulsante destro del mouse e scegliere **Riprendi**.

## Ripresa delle code tramite Shell

Per riprendere le code, utilizzare la sintassi seguente.
```powershell
    Resume-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>
```
In questo esempio vengono riprese tutte le code del server locale con lo stato Sospeso.

```powershell
Resume-Queue -Filter {Status -eq "Suspended"}
```

In questo esempio vengono riprese le code di recapito sospese denominate contoso.com sul server Mailbox01.

```powershell
Resume-Queue -Identity Mailbox01\contoso.com
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la ripresa di una coda sia stata eseguita correttamente, procedere come segue:

1.  Utilizzare il Visualizzatore code o il cmdlet **Get-Queue** per trovare la coda che si sta tentando di riprendere.

2.  Verificare che la proprietà della coda **Stato** non abbia il valore `Suspended`.

## Code dei tentativi

Quando un server di trasporto non riesce a connettersi all'hop successivo, la coda di recapito viene messa nello stato Riprova. Quando si esegue un nuovo tentativo di elaborazione di una coda di recapito utilizzando Visualizzatore code o Shell, vengono imposti un tentativo di connessione immediata e l'annullamento del successivo tentativo pianificato. Se la connessione non riesce, il timer dell'intervallo tra i tentativi viene reimpostato. L'azione avrà effetto solo se lo stato della coda di recapito è Riprova.

## Utilizzare il Visualizzatore code nella Casella degli strumenti di Exchange per riprendere una coda

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange 2013** \> **Casella degli strumenti di Exchange**.

2.  Nella sezione **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code** per aprire lo strumento in una nuova finestra.

3.  In Visualizzatore code, fare clic sulla scheda **Code**. Viene visualizzato un elenco di tutte le code presenti nel server a cui si è connessi.

4.  Fare clic su **Crea filtro** e immettere l'espressione del filtro nel modo seguente:
    
    1.  Selezionare **Stato** dall'elenco a discesa delle proprietà della coda.
    
    2.  Selezionare **Uguale a** dall'elenco a discesa degli operatori di confronto.
    
    3.  Selezionare **Riprova** dall'elenco a discesa dei valori.

5.  Scegliere **Applica filtro**. Verranno visualizzate tutte le code il cui stato corrente è **Riprova**.

6.  Selezionare una o più code dall'elenco. Fare clic con il pulsante destro del mouse e scegliere **Riprova coda**. Se il tentativo di connessione riesce, lo stato della coda cambia diventando **Attivo**. Se è impossibile stabilire la connessione, la coda rimarrà nello stato **Riprova** e l'ora del tentativo successivo verrà aggiornata.

## Esecuzione di un nuovo tentativo di elaborazione di una coda tramite Shell

Per riprovare le code, utilizzare la sintassi seguente.
```powershell
    Retry-Queue <-Identity QueueIdentity | -Filter QueueFilter [-Server ServerIdentity]>
```

Con questo esempio viene eseguito un nuovo tentativo di elaborazione di tutte le code sul server locale con lo stato Riprova.

```powershell
Retry-Queue -Filter {status -eq "retry"}
```

In questo esempio viene eseguito un nuovo tentativo di elaborazione della coda denominata contoso.com con lo stato `Retry` sul server Mailbox01.

```powershell
Retry-Queue -Identity Mailbox01\contoso.com
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il tentativo di elaborazione della coda sia stato eseguito correttamente, procedere come segue:

1.  Utilizzare il Visualizzatore code o il cmdlet **Get-Queue** per trovare la coda che si sta tentando di elaborare.

2.  Verificare che la proprietà **LastRetryTime** corrisponda all'ora in cui è stato effettuato il tentativo di elaborazione della coda.

## Reinvio dei messaggi in coda

Il reinvio di una coda è simile al tentativo di elaborazione, eccetto per i messaggi che vengono inviati nuovamente alla Coda di invio per la rielaborazione da parte del classificatore. È possibile reinviare manualmente i messaggi con il seguente stato:

  - Code di recapito con lo stato Riprova. I messaggi nelle code non devono essere nello stato Sospeso.

  - Messaggi nella coda non raggiungibile con stato diverso da Sospeso.

  - Messaggi nella coda di messaggi non elaborabili.

## Reinvio dei messaggi tramite Shell

Per reinviare i messaggi, utilizzare la sintassi seguente.
```powershell
    Retry-Queue <-Identity QueueIdentity | -Filter {Status -eq "Retry"} -Server ServerIdentity> -Resubmit $true
```
In questo esempio vengono reinviati tutti i messaggi posizionati in qualsiasi coda di recapito con lo stato Riprova sul server Mailbox01.

```powershell
Retry-Queue -Filter {Status -eq "Retry"} -Server Mailbox01 -Resubmit $true
```

In questo esempio vengono reinviati tutti i messaggi posizionati nella coda non raggiungibile sul server Mailbox01.

```powershell
Retry-Queue -Identity Mailbox01\Unreachable -Resubmit $true
```

## Reinvio dei messaggi dalla coda dei messaggi non elaborabili

È possibile reinviare i messaggi dalla coda dei messaggi non elaborabili riprendendo il messaggio. È possibile utilizzare il Visualizzatore code o Shell per reinviare i messaggi dalla coda dei messaggi non elaborabili. Tenere presente che è possibile visualizzare la coda dei messaggi non elaborabili solo nel Visualizzatore code quando in tale coda sono presenti messaggi.


> [!NOTE]
> La coda dei messaggi non elaborabili contiene i messaggi ritenuti dannosi per il sistema di Exchange dopo un problema del server. I messaggi potrebbero essere pericolosi sia per quanto ne riguarda il contenuto che il formato. In alternativa, potrebbero essere considerati pericolosi a seguito di un errore dovuto a un agente scritto in maniera non corretta, che ha provocato l'arresto anomalo del server Exchange durante l'elaborazione dei presunti messaggi errati. Se non si è certi della sicurezza dei messaggi nella coda dei messaggi non elaborabili, esportare i messaggi su file in modo da poterli esaminare. Per ulteriori informazioni, vedere <A href="export-messages-from-queues-exchange-2013-help.md">Esportazione dei messaggi dalle code</A>.



## Utilizzare il Visualizzatore code nella Casella degli strumenti di Exchange per reinviare i messaggi dalla coda di messaggi non elaborabili

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange 2013** \> **Casella degli strumenti di Exchange**.

2.  Nella sezione **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code** per aprire lo strumento in una nuova finestra.

3.  In Visualizzatore code, fare clic sulla scheda **Code**. Viene visualizzato un elenco di tutte le code presenti nel server a cui si è connessi.

4.  Fare clic sulla coda dei messaggi non elaborabili. Nel riquadro azioni, selezionare **Visualizza messaggi**.

5.  Selezionare uno o più messaggi dall'elenco, fare clic con il pulsante destro del mouse e selezionare **Riprendi**.

## Reinvio dei messaggi dalla coda dei messaggi non elaborabili tramite Shell

Per reinviare un messaggio dalla coda dei messaggi non elaborabili, attenersi alla seguente procedura.

1.  Trovare l'identità del messaggio eseguendo il comando seguente.
    
    ```powershell
        Get-Message -Queue Poison | Format-Table Identity
    ```

2.  Utilizzare l'identità del messaggio da un passaggio precedente nel seguente comando.
    
    ```powershell
        Resume-Message <PoisonMessageIdentity>
    ```
    
    In questo esempio viene ripristinato un messaggio dalla coda dei messaggi non elaborabili con il valore dell'identità del messaggio 222.
    
    ```powershell
        Resume-Message 222
    ```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver reinviato correttamente il messaggio dalla coda dei messaggi non elaborabili, procedere come segue:

1.  Utilizzare il Visualizzatore code o il cmdlet **Get-Queue** per visualizzare la coda di messaggi non elaborabili che si sta tentando di reinviare.

2.  Verificare che il messaggio non si trovi più nella coda dei messaggi non elaborabili. Tenere presente che una coda di messaggi non elaborabili vuota non viene visualizzata nel Visualizzatore code o nel cmdlet **Get-Queue**. Tuttavia, se il messaggio reinviato era l'unico messaggio presente nella coda dei messaggi non elaborabili e questa non è più visibile, significa che il messaggio è stato reinviato correttamente.

## Sospensione code

Sospendendo una coda, si impedisce ai messaggi di lasciare la coda ma non si cambia lo stato dei messaggi nella coda. I messaggi in fase di recapito tramite l'invio SMTP saranno portati a termine. È possibile sospendere una coda per interrompere il flusso di posta, quindi sospendere uno o più messaggi presenti nella coda. Quando si ripristina la coda, i messaggi sospesi non lasciano la coda.

È possibile sospendere una coda il cui stato sia Attivo o Riprova. Inoltre, è possibile sospendere la coda dei messaggi con destinatari non raggiungibili e la coda di invio.

Se si sospende la coda dei messaggi con destinatari non raggiungibili, gli elementi non verranno inviati nuovamente al classificatore quando il server di trasporto riceve gli aggiornamenti di configurazione finché la coda non verrà ripristinata. Se si sospende la coda di invio, i messaggi non verranno recuperati dal classificatore finché la coda non verrà ripristinata.

## Utilizzare il Visualizzatore code nella Casella degli strumenti di Exchange per sospendere una coda

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange 2013** \> **Casella degli strumenti di Exchange**.

2.  Nella sezione **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code** per aprire lo strumento in una nuova finestra.

3.  In Visualizzatore code, fare clic sulla scheda **Code**. Viene visualizzato un elenco di tutte le code presenti nel server a cui si è connessi. È possibile creare un filtro per visualizzare solo le code che soddisfano criteri specifici.

4.  Selezionare uno o più code, fare clic con il pulsante destro del mouse e scegliere **Sospendi**.

## Sospensione di una coda tramite Shell

Per sospendere una coda, utilizzare la seguente sintassi.
```powershell
    Suspend-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>
```
Con questo esempio vengono sospese tutte le code sul server locale il cui conteggio dei messaggi è uguale o maggiore di 1.000 e il cui stato è Riprova.

```powershell
Suspend-Queue -Filter {MessageCount -ge 1000 -and Status -eq "Retry"}
```

In questo esempio viene sospesa la coda denominata contoso.com sul server Mailbox01.

```powershell
Suspend-Queue -Identity Mailbox01\contoso.com
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la sospensione della coda sia stata eseguita correttamente, procedere come segue:

1.  Utilizzare il Visualizzatore code o il cmdlet **Get-Queue** per trovare la coda che si sta tentando di sospendere.

2.  Verificare che la proprietà della coda **Stato** abbia il valore `Suspended`.


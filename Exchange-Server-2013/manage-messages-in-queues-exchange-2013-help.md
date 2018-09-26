---
title: 'Gestione dei messaggi nelle code: Exchange 2013 Help'
TOCTitle: Gestione dei messaggi nelle code
ms:assetid: 83358884-6036-4e91-87a8-35200541874d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123535(v=EXCHG.150)
ms:contentKeyID: 51407392
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione dei messaggi nelle code

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-05-07_

In Microsoft Exchange Server 2013, è possibile utilizzare il Visualizzatore code nella Casella degli strumenti di Exchange oppure in Exchange Management Shell per gestire i messaggi nelle code. Per ulteriori informazioni sull'utilizzo dei cmdlet di gestione dei messaggi in Exchange Management Shell, vedere [Utilizzare Exchange Management Shell per gestire le code](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Code" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Per saperne di più

## Eliminazione dei messaggi dalle code

Un messaggio che viene inviato a più di un destinatario può essere situato in più di una coda. Per rimuovere un messaggio da più code in un'unica operazione, è necessario utilizzare un filtro. Quando si rimuovono i messaggi da una coda, è possibile scegliere se inviare un rapporto di mancato recapito (NDR, Non-Delivery Report). Non è possibile rimuovere un messaggio dalla coda di invio.

## Utilizzo del visualizzatore code nella Casella degli strumenti di Exchange per rimuovere i messaggi

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange 2013** \> **Casella degli strumenti di Exchange**.

2.  Nella sezione **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code** per aprire lo strumento in una nuova finestra.

3.  In Visualizzatore code, fare clic sulla scheda **Messaggi**. Viene visualizzato un elenco di tutti i messaggi presenti nel server a cui si è connessi. Per regolare l'azione per una singola coda, fare clic sulla scheda **Code**, fare doppio clic sul nome della coda e selezionare la scheda *Server\\Coda*.

4.  Selezionare uno o più messaggi dall'elenco, fare clic con il pulsante destro del mouse e scegliere **Rimuovi i messaggi (con rapporto di mancato recapito)** o **Rimuovi i messaggi (senza inviare rapporti di mancato recapito)**. Viene visualizzata una finestra di dialogo per confermare l'azione selezionata e in cui viene chiesto **Continuare?** Fare clic su **Sì**.

5.  Per rimuovere tutti i messaggi da una determinata coda, scegliere la scheda **Code**. Selezionare una coda, fare clic con il pulsante destro del mouse e scegliere **Rimuovi i messaggi (con rapporto di mancato recapito)** o **Rimuovi i messaggi (senza inviare rapporti di mancato recapito)**. Viene visualizzata una finestra di dialogo per confermare l'azione selezionata e in cui viene chiesto **Continuare?** Fare clic su **Sì**.
    

    > [!NOTE]
    > Se si utilizza un elenco filtrato, la pagina visualizzata può non includere tutte le voci nel filtro. In questo caso, viene visualizzato il messaggio: <STRONG>L'operazione influirà su tutti gli elementi nella pagina. Per espandere l'ambito dell'operazione e includere tutti gli elementi nel filtro, selezionare la casella seguente quindi scegliere OK.</STRONG>



## Rimozione dei messaggi tramite Shell

Per eliminare i messaggi dalle code, utilizzare la seguente sintassi.
```powershell
    Remove-Message <-Identity MessageIdentity | -Filter {MessageFilter}> -WithNDR <$true | $false>
```
Con questo esempio vengono eliminati i messaggi nelle code il cui oggetto è "Win Big" senza inviare un rapporto di mancato recapito.

```powershell
Remove-Message -Filter {Subject -eq "Win Big"} -WithNDR $false
```

Nell'esempio riportato viene rimosso il messaggio con ID messaggio 3 da una coda non raggiungibile sul server denominato Mailbox01 e viene inviato un rapporto di mancato recapito.

```powershell
Remove-Message -Identity Mailbox01\Unreachable\3 -WithNDR $true
```

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver rimosso correttamente i messaggi da una coda, effettuare una delle seguenti operazioni:

  - Nel visualizzatore di code, selezionare la coda oppure creare un filtro per verificare che i messaggi non siano più presenti.

  - Utilizzare il cmdlet **Get-Message** con i parametri *Queue* o *Filter* per verificare che i messaggi non siano più presenti. Per ulteriori informazioni, vedere [Get-Message](https://technet.microsoft.com/it-it/library/bb124738\(v=exchg.150\)).

## Riprendere messaggi nelle code

È possibile riprendere un messaggio il cui stato corrente è Sospeso. Riprendendo un messaggio, ne viene abilitato il recapito. Se si riprende un messaggio che si trova nella coda dei messaggi non elaborabili, il messaggio verrà inviato al classificatore per l'elaborazione. Un messaggio inviato a più destinatari potrebbe trovarsi in più code. Per riprendere un messaggio in più code con un'unica operazione è necessario utilizzare un filtro.

## Utilizzo del visualizzatore code nella Casella degli strumenti di Exchange per riprendere i messaggi

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange 2013** \> **Casella degli strumenti di Exchange**.

2.  Nella sezione **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code** per aprire lo strumento in una nuova finestra.

3.  In Visualizzatore code, fare clic sulla scheda **Messaggi**. Viene visualizzato un elenco di tutti i messaggi presenti nel server a cui si è connessi. Per regolare l'azione in modo che sia focalizzata su una singola coda, fare clic sulla scheda **Code**, fare doppio clic sul nome della coda e infine scegliere la scheda *Server\\Coda* che viene visualizzata.

4.  Fare clic su **Crea filtro** e immettere l'espressione del filtro nel modo seguente:
    
    1.  Selezionare **Stato** dall'elenco a discesa delle proprietà dei messaggi.
    
    2.  Selezionare **Uguale a** dall'elenco a discesa degli operatori di confronto.
    
    3.  Selezionare **Sospeso** dall'elenco a discesa dei valori.

5.  Scegliere **Applica filtro**. Verranno visualizzati tutti i messaggi il cui stato è Sospeso.

6.  Selezionare uno o più messaggi dall'elenco, fare clic con il pulsante destro del mouse e selezionare **Riprendi**.

## Riprendere i messaggi tramite Shell

Per riprendere i messaggi, utilizzare la sintassi seguente:

```powershell
Resume-Message <-Identity MessageIdentity | -Filter {MessageFilter}>
```

In questo esempio vengono ripresi tutti i messaggi inviati da qualsiasi mittente al dominio Contoso.com.
```powershell
    Resume-Message -Filter {FromAddress -eq "*contoso.com"}
```
In questo esempio viene ripreso il messaggio con l'ID messaggio 3 nella coda non raggiungibile sul server Hub01.

```powershell
Resume-Message -Identity Hub01\Unreachable\3
```

Per inviare di nuovo i messaggi nella coda dei messaggi non elaborabili, eseguire uno dei seguenti passaggi:

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver ripreso correttamente i messaggi nelle code, effettuare una delle seguenti operazioni:

  - Nel visualizzatore di code, selezionare la coda oppure creare un filtro per verificare che i messaggi non siano più in sospeso.

  - Utilizzare il cmdlet **Get-Message** con i parametri *Queue* o *Filter* per verificare che i messaggi non siano più in sospeso. Per ulteriori informazioni, vedere [Get-Message](https://technet.microsoft.com/it-it/library/bb124738\(v=exchg.150\)).

Tenere presente che se non è possibile trovare il messaggio in nessuna delle code sul server, probabilmente significa che il messaggio è stato correttamente recapitato all'hop successivo.

## Sospendere i messaggi nelle code

Quando si sospende un messaggio, ne viene impedito il recapito. Non verranno sospesi eventuali recapiti già in corso dei messaggi visualizzati nella coda. Il recapito verrà continuato e lo stato del messaggio sarà **PendingSuspend**. Se il recapito non riesce, il messaggio verrà reinserito nella coda e quindi verrà sospeso. Non è possibile sospendere un messaggio che si trova nella coda di invio o nella coda di messaggi non elaborabili.

Un messaggio inviato a più destinatari potrebbe trovarsi in più code. Per sospendere un messaggio in più code con un'unica operazione, è necessario utilizzare un filtro.

## Utilizzo del visualizzatore code nella Casella degli strumenti di Exchange per sospendere i messaggi

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange 2013** \> **Casella degli strumenti di Exchange**.

2.  Nella sezione **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code** per aprire lo strumento in una nuova finestra.

3.  In Visualizzatore code, fare clic sulla scheda **Messaggi**. Viene visualizzato un elenco di tutti i messaggi presenti nel server a cui si è connessi. Per limitare la visualizzazione a una singola coda, fare clic sulla scheda **Code**, fare doppio clic sul nome della coda, quindi fare clic sulla scheda *Server\\Coda* visualizzata.

4.  Selezionare uno o più messaggi, fare clic con il pulsante destro del mouse, quindi selezionare **Sospendi**.

## Sospensione dei messaggi tramite Shell

Per sospendere i messaggi, utilizzare la sintassi seguente:

```powershell
Suspend-Message <-Identity MessageIdentity | -Filter {MessageFilter}>
```

In questo esempio vengono sospesi tutti i messaggi nelle code provenienti da qualsiasi mittente nel dominio contoso.com.
```powershell
    Suspend-Message -Filter {FromAddress -eq "*contoso.com"}
```
In questo esempio viene sospeso il messaggio con l'ID messaggio 3 nella coda non raggiungibile sul server denominato Mailbox01:

```powershell
Suspend-Message -Identity Mailbox01\Unreachable\3
```

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver sospeso correttamente i messaggi nelle code, effettuare una delle seguenti operazioni:

  - Nel visualizzatore di code, selezionare la coda oppure creare un filtro per verificare che i messaggi siano in sospeso.

  - Utilizzare il cmdlet **Get-Message** con i parametri *Queue* o *Filter* per verificare che i messaggi siano in sospeso. Per ulteriori informazioni, vedere [Get-Message](https://technet.microsoft.com/it-it/library/bb124738\(v=exchg.150\)).


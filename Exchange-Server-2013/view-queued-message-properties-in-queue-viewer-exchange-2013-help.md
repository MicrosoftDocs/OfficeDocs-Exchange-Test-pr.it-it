---
title: 'Visualizzare le proprietà del messaggio in coda nel Visualizzatore di code: Exchange 2013 Help'
TOCTitle: Visualizzare le proprietà del messaggio in coda nel Visualizzatore di code
ms:assetid: 9d15d8b8-e061-4288-9354-df58e282fb6b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123934(v=EXCHG.150)
ms:contentKeyID: 50481278
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.Edge.SystemManager.MessagePropertyPage
ms.translationtype: MT
---

# Visualizzare le proprietà del messaggio in coda nel Visualizzatore di code

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-01-17_

È possibile utilizzare Visualizzatore code in Casella degli strumenti di Exchange per visualizzare le proprietà di un messaggio accodato per il recapito.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Code" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È anche possibile utilizzare il cmdlet Get-Message in Exchange Management Shell per visualizzare ulteriori proprietà dei messaggi che non sono visibili nel Visualizzatore code. Per ulteriori informazioni, vedere [Filtri per i messaggi](message-filters-exchange-2013-help.md) e [Utilizzare Exchange Management Shell per gestire le code](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare Visualizzatore code in Casella degli strumenti di Exchange per visualizzare le proprietà di un messaggio

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange 2013** \> **Casella degli strumenti di Exchange**.

2.  Nella sezione **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code** per aprire lo strumento in una nuova finestra.

3.  In Visualizzatore code, selezionare la scheda **Messaggi** per visualizzare l'elenco dei messaggi attualmente in coda per il recapito all'interno dell'organizzazione.

4.  Fare clic con il pulsante destro del mouse sul messaggio di cui si desidera visualizzare le proprietà, quindi selezionare **Proprietà**.

5.  
    
    Nella scheda **Generale**, vengono visualizzate le informazioni dettagliate sul messaggio.
    
      - **Identità**   In questo campo, viene visualizzato il valore intero rappresentante un particolare messaggio. L'identità del messaggio viene assegnata dal database di code quando il messaggio viene ricevuto per l'elaborazione. È possibile includere un server facoltativo e l'identità della coda per identificare un'istanza univoca del messaggio.
    
      - **Oggetto**   In questo campo, viene visualizzato l'oggetto di un messaggio, espresso come stringa di testo. Il valore viene ricavato dal campo dell'intestazione `Subject:`.
    
      - **ID messaggio Internet**   In questo campo, viene visualizzato il valore del campo di intestazione `MessageID:`. Il valore di questa proprietà viene espresso come un GUID seguito dall'indirizzo SMTP del server mittente, come nel seguente esempio: 67D754D6103DC4FB3BA6BC7205DACABA61231@exchange.contoso.com
    
      - **Indirizzo mittente**   In questo campo, viene visualizzato l'indirizzo SMTP del mittente del messaggio. Questo valore si ricava da MAIL FROM: nella busta del messaggio.
    
      - **Stato**   Questo campo mostra lo stato corrente del messaggio. Un messaggio può avere uno dei seguenti valori di stato:
        
          - **Attivo**   Se il messaggio si trova in una coda di recapito, sarà recapitato alla destinazione indicata. Se il messaggio si trova nella coda di invio, sarà elaborato dal classificatore.
        
          - **In attesa di rimozione**   Il messaggio è stato eliminato dall'amministratore ma era già in fase di recapito. Il messaggio sarà eliminato se l'operazione di recapito termina con un errore che determina la ricollocazione del messaggio nella coda. In caso contrario, il messaggio viene recapitato.
        
          - **In attesa di sospensione**   Il messaggio è stato sospeso dall'amministratore ma era già in fase di recapito. Il messaggio sarà sospeso se l'operazione di recapito termina con un errore che determina la ricollocazione del messaggio nella coda. In caso contrario, il messaggio viene recapitato.
        
          - **Pronto**   Il messaggio è in attesa nella coda ed è pronto per l'elaborazione.
        
          - **Riprova**   L'ultimo tentativo di collegamento per la coda in cui si trova il messaggio non ha avuto esito positivo. Il messaggio è in attesa del prossimo tentativo di accodamento.
        
          - **Sospeso**   Il messaggio è stato sospeso dall'amministratore.
    
      - **Dimensione (KB)**   In questo campo, le dimensioni del messaggio vengono arrotondate per eccesso al kilobyte (KB).
    
      - **Nome origine messaggio**   In questo campo, viene visualizzato il nome del componente che ha inviato il messaggio alla coda.
    
      - **IP di origine**   In questo campo, viene visualizzato l'indirizzo IP del server esterno che ha inviato il messaggio all'organizzazione di Exchange.
    
      - **SCL**   In questo campo, viene visualizzato il livello di probabilità di posta indesiderata (SCL, Spam Confidence Level) del messaggio. Le voci SCL valide sono numeri interi da 0 a 9 e -1. Una voce SCL vuota indica che il messaggio non è stato elaborato dall'agente filtro contenuto.
    
      - **Data ricezione**   In questo campo, sono indicate la data e l'ora in cui il messaggio è stato ricevuto dal server che contiene la coda in cui si trova il messaggio.
    
      - **Data scadenza**   In questo campo, viene visualizzata la data/ora in cui il messaggio scade e viene eliminato dalla coda se non può essere recapitato.
    
      - **Ultimo errore**   Questo campo mostra l'ultimo errore registrato per il messaggio.
    
      - **ID coda**   In questo campo, viene visualizzata l'identità della coda contenente il messaggio. L'identità della coda viene espressa come *Server\\destinazione* dove *destinazione* è un gruppo di recapito, una destinazione di routing, un nome di coda persistente o l'identificatore del database delle code. L'identificatore del database delle code è rappresentato come un numero intero e può essere determinato visualizzando le proprietà del messaggio.
    
      - **Destinatari**   In questo campo, viene visualizzato l'elenco di destinatari a cui è indirizzato il messaggio.
    
      - **Numero tentativi**   In questo campo, viene visualizzato il numero di tentativi di invio di un messaggio a una destinazione.

6.  
    
    Nella scheda **Informazioni destinatario**, vengono visualizzate le seguenti informazioni sui destinatari del messaggio.
    
      - **Indirizzo**   In questo campo, viene visualizzato l'indirizzo SMTP del destinatario del messaggio. Questo valore viene ricavato da `RCPT TO:` nella busta del messaggio.
    
      - **Stato**   Questo campo mostra lo stato corrente del messaggio. Un messaggio può assumere uno dei seguenti valori di stato:
        
          - **Attivo**   Se il messaggio si trova in una coda di recapito, sarà recapitato alla destinazione indicata. Se il messaggio si trova nella coda di invio, sarà elaborato dal classificatore.
        
          - **In attesa di rimozione**   Il messaggio è stato eliminato dall'amministratore ma era già in fase di recapito. Il messaggio sarà eliminato se l'operazione di recapito termina con un errore che determina la ricollocazione del messaggio nella coda. In caso contrario, il messaggio viene recapitato.
        
          - **In attesa di sospensione**   Il messaggio è stato sospeso dall'amministratore ma era già in fase di recapito. Il messaggio sarà sospeso se l'operazione di recapito termina con un errore che determina la ricollocazione del messaggio nella coda. In caso contrario, il messaggio viene recapitato.
        
          - **Pronto**   Il messaggio è in attesa nella coda ed è pronto per l'elaborazione.
        
          - **Riprova**   L'ultimo tentativo di collegamento per la coda in cui si trova il messaggio non ha avuto esito positivo. Il messaggio è in attesa del prossimo tentativo di accodamento.
        
          - **Sospeso**   Il messaggio è stato sospeso dall'amministratore.
    
      - **Ultimo errore**   Questo campo mostra l'ultimo errore registrato per il messaggio.

## Visualizzazione delle proprietà di un messaggio tramite Shell

È possibile utilizzare il cmdlet **Get-Message** per visualizzare le proprietà di un messaggio attualmente in coda per il recapito. Nell'esempio seguente, vengono catalogati l'indirizzo del mittente, i destinatari, l'oggetto e le informazioni sulla data di ricezione per tutti i messaggi che si trovano attualmente nello stato di Riprova:

    Get-Message -IncludeRecipientInfo -Filter {Status -eq "Retry"} | Format-Table FromAddress,Recipients,Subject,DateReceived

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-Message](https://technet.microsoft.com/it-it/library/bb124738\(v=exchg.150\)).


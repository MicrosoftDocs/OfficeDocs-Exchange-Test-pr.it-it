---
title: 'Crea connett. ricezione posta da Internet: Exchange 2013 Help'
TOCTitle: Creare un connettore di ricezione per la ricezione di posta elettronica da Internet
ms:assetid: 534bbd32-a0db-4d50-9579-4933b156d7b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657447(v=EXCHG.150)
ms:contentKeyID: 50480604
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un connettore di ricezione per la ricezione di posta elettronica da Internet

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-15_

In questa procedura è spiegato come configurare un connettore di ricezione per ricevere i messaggi di posta elettronica da Internet.


> [!NOTE]
> Nella maggior parte dei casi, non sarà necessario configurare esplicitamente un connettore di ricezione per la posta da Internet, perché un connettore di questo tipo viene implicitamente creato durante l'installazione di Exchange. Per ulteriori informazioni, vedere <A href="receive-connectors-exchange-2013-help.md">Connettori di ricezione</A>.



Ulteriori informazioni sugli scenari in cui si utilizza questa procedura Vedere i seguenti argomenti:

  - [Configurazione del flusso di posta e di Accesso client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di ricezione" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Vedere [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) se si è in fase di inizio dell'installazione. Dopo l'installazione, è possibile utilizzare le procedure riportate in questo argomento per creare il connettore di ricezione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo dell'interfaccia di amministrazione di Exchange per la creazione di un connettore di ricezione per ricevere i messaggi da Internet

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Connettori di ricezione**. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per creare un connettore di ricezione.

2.  Nella pagina **Nuovo connettore di ricezione**, specificare un nome per il connettore di ricezione e quindi selezionare **Trasporto Frontend** per **Ruolo**. Poiché in questo caso la posta proviene da Internet, inizialmente è consigliabile instradarla al server o ai server Front End per semplificare e consolidare il flusso di posta.

3.  Scegliere **Internet** come tipo. Il connettore di ricezione riceverà la posta dai mittenti su Internet.

4.  Per **Binding scheda di rete**, notare che **Tutti gli IPv4 disponibili** compare nell'elenco **Indirizzi IP** e **Porta** è impostata su 25. (il protocollo SMTP utilizza la porta 25.) Questo indica che il connettore attende le connessioni su tutti gli indirizzi IP assegnati alle schede di rete sul server locale.
    

    > [!NOTE]
    > In presenza di più schede di rete, in questa pagina è possibile, ma non necessario, aggiungere un indirizzo IP assegnato a una specifica scheda di rete sul server locale.



5.  Fare clic sul pulsante **Fine** per creare il connettore.

Dopo aver creato il connettore di ricezione, apparirà nell'elenco dei connettori di ricezione. Se si desidera vedere un esempio di come creare un connettore di ricezione con un cmdlet, vedere [New-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125139\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il connettore di ricezione per i messaggi provenienti da Internet sia stato creato correttamente, provare a inviare un messaggio da una fonte esterna e controllare che gli utenti lo ricevano senza problemi. Se è possibile ricevere la posta, la configurazione funziona correttamente.

## Ulteriori informazioni

[Creare un connettore di ricezione protetto per la ricezione di posta elettronica da un partner](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

[Creare un connettore di ricezione per la ricezione di posta elettronica da un sistema non è in esecuzione Exchange](create-a-receive-connector-to-receive-email-from-a-system-not-running-exchange-exchange-2013-help.md)


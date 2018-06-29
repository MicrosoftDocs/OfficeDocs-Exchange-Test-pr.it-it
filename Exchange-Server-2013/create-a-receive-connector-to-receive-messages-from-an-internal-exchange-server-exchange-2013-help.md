---
title: 'Creare un connettore di ricezione per ricevere messaggi da un server Exchange interno: Exchange 2013 Help'
TOCTitle: Creare un connettore di ricezione per ricevere messaggi da un server Exchange interno
ms:assetid: 546cead9-7a2d-4332-a5f6-35343d56c619
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657448(v=EXCHG.150)
ms:contentKeyID: 50480618
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un connettore di ricezione per ricevere messaggi da un server Exchange interno

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-03_

Un connettore di ricezione di tipo **Interno** viene creato quando si desidera ricevere la posta da un server Exchange. Utilizzare questo tipo di connettore per controllare l'instradamento della posta all'interno dell'organizzazione: ad esempio, se si desidera instradare la posta dal servizio di trasporto su un server Cassette postali a uno specifico server Trasporto Edge oppure da un server Cassette postali a un altro.

Ulteriori informazioni sugli scenari in cui si utilizza questa procedura Vedere i seguenti argomenti:

  - [Configurazione del flusso di posta e di Accesso client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di ricezione" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Vedere [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) se si è in fase di inizio dell'installazione. Dopo l'installazione, è possibile utilizzare le procedure riportate in questo argomento per creare il connettore di ricezione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Creare un connettore di ricezione per ricevere messaggi da un server Exchange interno

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Connettori di ricezione**. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per creare un nuovo connettore di ricezione.

2.  Nella pagina **Nuovo connettore di ricezione**, specificare un nome per il connettore di ricezione e quindi selezionare **Trasporto Hub** per **Ruolo**. In questo caso si presuppone che si desideri instradare la posta all'interno della rete, non all'interno e all'esterno dell'organizzazione.

3.  Scegliere **Interno** come tipo. Il connettore è configurato con l'autenticazione del server Exchange.

4.  Se le pagina delle impostazioni della rete remota elenca 0.0.0.0-255.255.255.255, il che significa che il connettore di ricezione riceve le connessioni da tutti gli indirizzi IP, fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi") per rimuoverlo. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), aggiungere l'indirizzo IP del server che dovrà ricevere la posta (ad esempio, 192.168.1.1) e fare clic su **Salva**.

5.  Fare clic su **Fine** per creare il connettore.

Dopo aver creato il connettore di ricezione, apparirà nell'elenco dei connettori di ricezione. Se si desidera vedere un esempio di come creare un connettore di ricezione con un cmdlet, vedere [New-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125139\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il connettore di ricezione per i messaggi provenienti da un server interno sia stato creato correttamente, controllare che i messaggi inviati dal server mittente raggiungano il server di destinazione senza problemi. Per fare ciò, è possibile utilizzare Exchange Management Shell e il cmdlet [Set-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125140\(v=exchg.150\)) per impostare *ProtocolLoggingLevel* per il connettore di ricezione appena creato su `Verbose` e quindi controllare i registri per verificare che il messaggio sia stato recapitato.

## Ulteriori informazioni

[Creare un connettore di ricezione per la ricezione di posta elettronica da Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

[Creare un connettore di ricezione protetto per la ricezione di posta elettronica da un partner](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)


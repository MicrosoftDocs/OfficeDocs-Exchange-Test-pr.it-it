---
title: 'Creare un connettore di ricezione protetto per la ricezione di posta elettronica da un partner: Exchange 2013 Help'
TOCTitle: Creare un connettore di ricezione protetto per la ricezione di posta elettronica da un partner
ms:assetid: 06aa692c-7940-4a14-a722-058c47440f85
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673037(v=EXCHG.150)
ms:contentKeyID: 50479936
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un connettore di ricezione protetto per la ricezione di posta elettronica da un partner

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

In questa procedura è spiegato come configurare un connettore di ricezione per ricevere in modo sicuro i messaggi di posta elettronica da un partner. Utilizzare questa procedura quando è necessario crittografare le comunicazioni con un partner attendibile. Il connettore deve essere configurato per accettare le connessioni esclusivamente da server che eseguono l'autenticazione tramite TLS (Transport Layer Security).

Ulteriori informazioni sugli scenari in cui si utilizza questa procedura Vedere i seguenti argomenti:

  - [Configurazione del flusso di posta e di Accesso client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di ricezione" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Vedere [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) se si è in fase di inizio dell'installazione. Dopo l'installazione, è possibile utilizzare le procedure riportate in questo argomento per creare il connettore di ricezione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo dell'interfaccia di amministrazione di Exchange per la creazione di un connettore di ricezione per ricevere in modo sicuro i messaggi da un partner

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Connettori di ricezione**. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per creare un nuovo connettore di ricezione.

2.  Nella pagina **Nuovo connettore di ricezione**, specificare un nome per il connettore di ricezione e quindi selezionare **Trasporto Frontend** per **Ruolo**. Poiché in questo caso la posta proviene da un partner, inizialmente è consigliabile instradarla al server Front End per semplificare e consolidare il flusso di posta.

3.  Scegliere **Partner** come tipo. Il connettore di ricezione riceverà la posta da un terzo attendibile.

4.  Per **Binding scheda di rete**, notare che **Tutti gli IPv4 disponibili** compare nell'elenco **Indirizzi IP** e **Porta** è impostata su 25. (il protocollo SMTP utilizza la porta 25.) Questo indica che il connettore attende le connessioni su tutti gli indirizzi IP assegnati alle schede di rete sul server locale. Fare clic su **Avanti**.

5.  Se le pagina delle impostazioni della rete remota elenca 0.0.0.0-255.255.255.255, il che significa che il connettore di ricezione riceve le connessioni da tutti gli indirizzi IP, fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi") per rimuoverlo. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), aggiungere l'indirizzo IP del server del partner e fare clic su **Salva**.
    

    > [!NOTE]
    > È anche possibile specificare un intervallo di indirizzi IP con una notazione CIDR (ad esempio, 64.4.6.100/24).



6.  Fare clic su **Fine** per creare il connettore.

Dopo aver creato il connettore di ricezione, apparirà nell'elenco dei connettori di ricezione. Se si desidera vedere un esempio di come creare un connettore di ricezione con un cmdlet, vedere [New-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125139\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il connettore di ricezione per i messaggi provenienti da un partner sia stato creato correttamente, controllare che il partner possa inviare la posta a uno degli utenti e che questo la riceva senza problemi. Se si riesce a ricevere posta crittografata (controllare l'intestazione del messaggio per verificare che sia utilizzato il protocollo TLS), significa che la configurazione è stata completata correttamente.

## Ulteriori informazioni

[Connettori di ricezione](receive-connectors-exchange-2013-help.md)


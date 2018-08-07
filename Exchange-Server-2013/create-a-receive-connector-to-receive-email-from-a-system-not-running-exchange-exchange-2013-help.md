---
title: 'Crea connet. ricez. posta da sistema non in esec. Exchange: Exchange 2013 Help'
TOCTitle: Creare un connettore di ricezione per la ricezione di posta elettronica da un sistema non è in esecuzione Exchange
ms:assetid: 85f0864a-6502-49db-8804-16755a7292b4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657467(v=EXCHG.150)
ms:contentKeyID: 50481099
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un connettore di ricezione per la ricezione di posta elettronica da un sistema non è in esecuzione Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

Potrebbe verificarsi una situazione in cui si desidera ricevere messaggi da un sistema che non utilizza Exchange. Ad esempio, potrebbe essere disponibile un dispositivo di rete che esegue i controlli sui criteri e poi instrada i messaggi al server di Exchange. In questo caso si presume che il dispositivo utilizzi SMTP. In caso contrario, è opportuno utilizzare un connettore esterno o un connettore dell'agente di recapito.

Ulteriori informazioni sugli scenari in cui si utilizza questa procedura Vedere i seguenti argomenti:

  - [Configurazione del flusso di posta e di Accesso client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di ricezione" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Vedere [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) se si è in fase di inizio dell'installazione. Dopo l'installazione, è possibile utilizzare le procedure riportate in questo argomento per creare il connettore di ricezione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare EAC per creare un connettore di ricezione per ricevere i messaggi da un dispositivo di messaggistica

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Connettori di ricezione**. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per creare un connettore di ricezione.

2.  Nella pagina **Nuovo connettore di ricezione**, specificare un nome per il connettore di ricezione e quindi selezionare **Trasporto Hub** per **Ruolo**. In questo caso, si desidera che il server Cassette postali esegua il servizio Trasporto per ricevere i messaggi dal dispositivo.

3.  Scegliere **Personalizzato** per il tipo, visto che il connettore di ricezione riceverà la posta elettronica da un dispositivo che non utilizza Microsoft Exchange Server 2013.

4.  Per **Binding scheda di rete**, verificare che sia elencato **Tutti gli IPv4 disponibili** nell'elenco **Indirizzi IP**. Fare clic su **Avanti**.

5.  Per **Impostazioni della rete remota**, fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi") per rimuovere **0.0.0.0-255.255.255.255** dall'elenco **Indirizzi IP**, visto che si desidera specificare che il connettore accetterà messaggi di posta elettronica da un dispositivo specifico. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere un nuovo indirizzo IP, quindi specificare l'indirizzo IP del dispositivo nella finestra **Aggiungi indirizzo IP**. Fare clic su **Salva**.

6.  Fare clic sul pulsante **Fine** per creare il connettore.

Dopo aver creato il connettore di ricezione, apparirà nell'elenco dei connettori di ricezione. Se si desidera vedere un esempio di come creare un connettore di ricezione con un cmdlet, vedere [New-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125139\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione di un connettore di ricezione per la ricezione di messaggi da un dispositivo di messaggistica, eseguire un test di ricezione della posta elettronica dal dispositivo. Se è possibile ricevere la posta, la configurazione funziona correttamente.

## Ulteriori informazioni

[Creare un connettore di ricezione per la ricezione di posta elettronica da Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)


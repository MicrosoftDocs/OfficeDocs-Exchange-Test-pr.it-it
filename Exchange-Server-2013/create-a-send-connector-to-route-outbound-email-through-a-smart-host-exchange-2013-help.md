---
title: 'Creare un connettore di invio per instradare la posta elettronica in uscita tramite uno Smart Host: Exchange 2013 Help'
TOCTitle: Creare un connettore di invio per instradare la posta elettronica in uscita tramite uno Smart Host
ms:assetid: 4a9ef08e-bd62-4c6b-8790-d24fb0f8f24b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673059(v=EXCHG.150)
ms:contentKeyID: 50480542
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creare un connettore di invio per instradare la posta elettronica in uscita tramite uno Smart Host

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-02-07_

In alcune situazioni è possibile che si desideri instradare la posta elettronica tramite uno smart host di terzi, ad esempio nel caso in cui si utilizzi un'applicazione di rete per eseguire i controlli dei criteri sui messaggi in uscita.


> [!NOTE]
> Lo smart host di terzi deve utilizzare il trasporto SMTP. In caso contrario, utilizzare un connettore esterno o un connettore agente di recapito.



Ulteriori informazioni sugli scenari in cui si utilizza questa procedura Vedere i seguenti argomenti:

  - [Configurazione del flusso di posta e di Accesso client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di invio" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Vedere [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) se si è in fase di inizio dell'installazione. Dopo l'installazione, è possibile utilizzare le procedure riportate in questo argomento per creare il connettore in uscita.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo dell'interfaccia di amministrazione di Exchange per la creazione di un connettore di invio per l'instradamento della posta in uscita tramite uno smart host

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Flusso di posta** \> **Connettori di invio**,quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella procedura guidata **Nuovo connettore di invio**, specificare un nome per il connettore di invio e quindi selezionare **Personalizzato** per **Tipo**. Generalmente si procede in questo modo quando si desidera instradare i messaggi a computer che non utilizzano Microsoft Exchange Server 2013. Fare clic su **Avanti**.

3.  Selezionare **Instrada la posta tramite smart host**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **Aggiungi smart host**, specificare l'indirizzo IP (ad esempio, 192.168.100.1) o il nome di dominio completo (ad esempio, contoso.com). Fare clic su **Salva**.
    
    Per **Autenticazione smart host**, scegliere il tipo di autenticazione richiesta dallo smart host. Se si sceglie **Autenticazione Basic**, è necessario fornire un nome utente e una password.
    

    > [!NOTE]
    > Se si sceglie Autenticazione Basic, è consigliabile utilizzare una connessione crittografata perché il nome utente e la password vengono inviati come testo normale.



4.  In **Spazio degli indirizzi**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **Aggiungi dominio**, controllare che sia indicato SMTP come **Tipo**. Per **Nome di dominio completo (FQDN)**, immettere \* per indicare che questo connettore di invio deve essere applicato ai messaggi inviati a qualsiasi dominio. Fare clic su **Salva**.

5.  In **Server di origine**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **Seleziona un server**, scegliere un server e fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Fare clic su **OK**.

6.  Fare clic su **Fine**.

Dopo aver creato il connettore di invio, questo apparirà nell'elenco dei connettori di invio.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente creato un connettore di invio per l'instradamento dei messaggi in uscita tramite uno smart host, inviare un messaggio da un utente nell'organizzazione (è possibile utilizzare Outlook Web App) al dominio specificato per **Spazio degli indirizzi**. Se il destinatario riceve il messaggio, il connettore di invio è stato configurato correttamente.

## Ulteriori informazioni

[Creare un connettore di invio per la posta elettronica inviato a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Connettori di invio](send-connectors-exchange-2013-help.md)


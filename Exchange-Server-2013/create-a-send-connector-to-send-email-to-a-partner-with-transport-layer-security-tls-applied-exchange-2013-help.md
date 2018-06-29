---
title: "Creare un connettore di invio per l'invio di posta elettronica a un partner con sicurezza TLS (Transport Layer) applicate: Exchange 2013 Help"
TOCTitle: Creare un connettore di invio per l'invio di posta elettronica a un partner con sicurezza TLS (Transport Layer) applicate
ms:assetid: ff2abefc-dd3e-4431-b947-df942fbf82d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657514(v=EXCHG.150)
ms:contentKeyID: 50482136
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un connettore di invio per l'invio di posta elettronica a un partner con sicurezza TLS (Transport Layer) applicate

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-15_

Per garantire comunicazioni sicure crittografate con un partner, è possibile creare un connettore di invio configurato per l'applicazione della crittografia TLS (Transport Layer Security) per i messaggi inviati a un dominio partner. TLS fornisce comunicazioni sicure in Internet.

Ulteriori informazioni sugli scenari in cui si utilizza questa procedura Vedere i seguenti argomenti:

  - [Configurazione del flusso di posta e di Accesso client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di invio" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Vedere [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) se si è in fase di inizio dell'installazione. Dopo l'installazione, è possibile utilizzare le procedure riportate in questo argomento per creare il connettore in uscita.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Creazione tramite l'interfaccia di aministrazione di Exchange di un connettore di invio per inviare posta elettronica con crittografia TLS a un partner

Per creare un connettore di invio in questo scenario, accedere all'interfaccia di amministrazione di Exchange e attenersi alla seguente procedura:

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Flusso di posta** \> **Connettori di invio**,quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella procedura guidata **Nuovo connettore di invio** specificare un nome per il connettore di invio e selezionare **Partner** per **Tipo**. Quando si seleziona **Partner**, il connettore viene configurato per consentire le connessioni solo ai server che eseguono l'autenticazione con certificati TLS. Fare clic su **Avanti**.

3.  Verificare che sia selezionato **Record MX associato con il dominio del destinatario**, che specifica che il connettore utilizza DNS (Domain Name System) per instradare la posta. Fare clic su **Avanti**.

4.  In **Spazio degli indirizzi**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **Aggiungi dominio**, controllare che sia indicato SMTP come **Tipo**. In **Nome di dominio completo (FQDN)** immettere il nome del dominio partner. Fare clic su **Salva**.

5.  In **Server di origine**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **Seleziona un server**, selezionare un server Cassette postali che verrà utilizzato per inviare la posta elettronica su Internet tramite il server Accesso client e fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Dopo aver selezionato il server, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Fare clic su **OK**.

6.  Fare clic su **Fine**.

Dopo aver creato il connettore di invio, apparirà nell'elenco dei connettori di invio.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il connettore di invio della posta elettronica con crittografia TLS a un partner sia stato creato correttamente, inviare un messaggio da un utente dell'organizzazione a un destinatario dell'organizzazione partner. Se il destinatario riceve il messaggio, la creazione del connettore è andata a buon fine.

## Ulteriori informazioni

[Creare un connettore di invio per la posta elettronica inviato a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Creare un connettore di invio per instradare la posta elettronica in uscita tramite uno Smart Host](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)


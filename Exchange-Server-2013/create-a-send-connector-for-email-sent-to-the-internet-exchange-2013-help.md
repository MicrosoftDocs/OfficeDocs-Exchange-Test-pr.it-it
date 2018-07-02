---
title: 'Creare un connettore di invio per la posta elettronica inviato a Internet: Exchange 2013 Help'
TOCTitle: Creare un connettore di invio per la posta elettronica inviato a Internet
ms:assetid: 6deaefa8-1152-40d9-b1ba-9c19bdf8a928
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657457(v=EXCHG.150)
ms:contentKeyID: 50480836
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un connettore di invio per la posta elettronica inviato a Internet

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-23_

Per impostazione predefinita, Microsoft Exchange Server 2013 non consente di inviare posta di fuori del dominio. Per inviare posta di fuori del dominio, è necessario creare un connettore di invio. Il grafico seguente illustra il flusso della posta quando si crea un connettore di invio per inviare posta a Internet.

![connector\_send\_onprem\_internet](images/JJ657457.e8963e4f-7dce-461f-bbcf-660278cefa35(EXCHG.150).gif "connector_send_onprem_internet")

Ulteriori informazioni sugli scenari in cui si utilizza questa procedura Vedere i seguenti argomenti:

  - [Configurazione del flusso di posta e di Accesso client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di invio" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Vedere [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) se si è in fase di inizio dell'installazione. Dopo l'installazione, è possibile utilizzare le procedure riportate in questo argomento per creare il connettore in uscita.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare EAC per creare un connettore di invio per la posta elettronica inviato a Internet

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Flusso di posta** \> **Connettori di invio**,quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella procedura guidata **nuovo connettore di invio** specificare un nome per il connettore di invio e quindi selezionare **Internet** per il **tipo**. Fare clic su **Avanti**.

3.  Verificare che sia selezionato **Record MX associato con il dominio del destinatario**, che specifica che il connettore utilizza DNS (Domain Name System) per instradare la posta. Fare clic su **Avanti**.

4.  In **spazio degli indirizzi**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **Aggiungi dominio** verificare che SMTP è elencato come **tipo**. Per **Nome dominio nome completo (FQDN)**, immettere \*, che indica che il connettore di invio viene applicata ai messaggi indirizzati a qualsiasi dominio. Fare clic su **Salva**.

5.  Verificare che **nell'ambito dei connettori di invio** non è selezionata e quindi fare clic su **Avanti**.

6.  In **Server di origine**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **Seleziona un server**, selezionare un server Cassette postali che verrà utilizzato per inviare la posta elettronica su Internet tramite il server Accesso client e fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Dopo aver selezionato il server, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Fare clic su **OK**.

7.  Fare clic su **Fine**.

Dopo aver creato il connettore di invio, apparirà nell'elenco dei connettori di invio.

## Utilizzo della Shell per instradare la posta tramite il server Accesso Client

In Exchange 2013 è possibile utilizzare il parametro *FrontendProxyEnabled* del cmdlet **Set-SendConnector** per instradare i messaggi in uscita tramite il server Accesso Client. Questo parametro non è impostato su `$true` per impostazione predefinita, ma in molti casi può consolidare e semplificare il flusso di posta, in particolare se si sta utilizzando un ambiente con un numero elevato di server di messaggistica.

In questo esempio viene impostato il parametro *FrontendProxyEnabled*`$true` su un connettore di invio.

    Set-SendConnector "Contoso.com Send Connector" -FrontendProxyEnabled $true

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver creato correttamente un connettore di invio per la posta elettronica inviato a Internet, inviare posta elettronica da uno degli utenti a un destinatario esterno e verificare che il messaggio viene recapitato correttamente.

## Ulteriori informazioni

[Connettori di invio](send-connectors-exchange-2013-help.md)

[Creare un connettore di invio per instradare la posta elettronica in uscita tramite uno Smart Host](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)


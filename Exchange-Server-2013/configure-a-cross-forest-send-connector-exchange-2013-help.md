---
title: 'Configurare un connettore di invio tra foreste: Exchange 2013 Help'
TOCTitle: Configurare un connettore di invio tra foreste
ms:assetid: 7840d172-071e-4f13-9379-2fe1eee1a7cc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945053(v=EXCHG.150)
ms:contentKeyID: 52063076
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare un connettore di invio tra foreste

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-02-21_

In Active Directory, la *foresta* rappresenta il limite esterno del servizio directory. È possibile creare connettori di invio per abilitare la comunicazione tra foreste. Nell'esempio riportato, i connettori utilizzano l'autenticazione di base.

Per le attività di gestione aggiuntive relative alla configurazione dei connettori, vedere [Connettori](connectors-exchange-2013-help.md).

Ulteriori informazioni sugli scenari in cui si utilizza questa procedura Vedere i seguenti argomenti:

  - [Distribuzione di Exchange 2013 in una topologia a più foreste](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 20 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di invio" e "Connettori di ricezione" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Vedere [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) se si è in fase di inizio dell'installazione. Dopo l'installazione, è possibile utilizzare la procedura riportata in questo argomento per creare i connettori per la configurazione di una topologia con più foreste.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Per saperne di più

## Creazione di un account utente in ogni foresta

È necessario creare un account utente in ogni foresta per utilizzare l'autenticazione di base. Creare un account in ogni foresta e aggiungerlo al gruppo di protezione universale di Exchange Server utilizzato per la comunicazione. Questo account viene utilizzato dal connettore di invio per l'autenticazione al server di posta ricevente nell'altra foresta. Ad esempio, è possibile fornire all'account utente al quale è associato il nome dell'entità utente FourthCoffee@Contoso.com le credenziali per l'autenticazione che il server Exchange utilizzano nel dominio Fourth Coffee quando viene inviata posta al server Exchange nel dominio Contoso.

## Utilizzo dell'interfaccia di amministrazione di Exchange per la creazione di un connettore di invio per l'instradamento della posta a un'altra foresta Exchange 2013

Stabilire un flusso di posta con più foreste tramite l'autenticazione di base.

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **flusso di posta** \> **connettori di invio**. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella procedura guidata **nuovo connettore di invio**, specificare un nome per il connettore di invio, quindi selezionare **Interno** per **Tipo**. Fare clic su **avanti**.

3.  Selezionare **Instrada la posta tramite smart host**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **aggiungi SmartHost**, specificare l'indirizzo IP del server di destinazione nella seconda foresta, ad esempio 64.4.6.100. Fare clic su **salva**, quindi su **avanti**.
    
    Per **Autenticazione smart host**, scegliere **Autenticazione di base** e fornire nome utente e password. In questa sezione è possibile scegliere **Consenti autenticazione di base solo dopo l'avvio di TLS** per comunicazioni protette in TLS.
    

    > [!NOTE]
    > Se si utilizza l'autenticazione di base in TLS, il server di destinazione deve essere configurato per utilizzare un certificato X.509.



4.  In **Spazio degli indirizzi**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **aggiungi dominio**, controllare che sia indicato SMTP come **Tipo**. Per **Nome di dominio completo (FQDN)**, immettere il dominio di destinazione, ad esempio fourthcoffee.com. Fare clic su **salva**, quindi su **avanti**.

5.  In **Server di origine**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **Seleziona un server**, scegliere il server da utilizzare e fare clic su **aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Fare clic su **ok**.

6.  Fare clic su **fine**. Il connettore viene visualizzato nell'elenco dei connettori di invio.

Dopo aver creato il connettore di invio, creare un connettore di invio nella seconda foresta che invii posta alla foresta originale. In questo caso, il nome di dominio completo (FQDN) specificato sarà il nome di dominio della prima foresta. Ad esempio, contoso.com.

## Impostazione delle autorizzazioni del secondo connettore tramite Shell

In questo esempio viene utilizzato lo script Enable-CrossForestConnector.ps1 in Shell per impostare le autorizzazioni sul connettore di invio per l'utilizzo in una topologia con più foreste.

    .\Enable-CrossForestConnector.ps1 -Connector "Cross-Forest" -user "ANONYMOUS LOGON"

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver correttamente creato connettori di invio per l'instradamento della posta elettronica nella seconda foresta, inviare un messaggio da un utente nell'organizzazione (è possibile utilizzare Outlook Web App) al dominio specificato per **Spazio degli indirizzi**. Se il destinatario riceve il messaggio, il connettore di invio è stato configurato correttamente.

## Ulteriori informazioni

[Creare un connettore di invio per la posta elettronica inviato a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Connettori di invio](send-connectors-exchange-2013-help.md)


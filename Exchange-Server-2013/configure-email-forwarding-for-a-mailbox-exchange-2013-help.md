---
title: 'Configura inoltro posta per cassetta postale: Exchange 2013 Help'
TOCTitle: Configurazione dell'inoltro della posta elettronica per una cassetta postale
ms:assetid: c7a7afaf-577e-49d6-8cee-bb4c4a5d570b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351134(v=EXCHG.150)
ms:contentKeyID: 50555691
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurazione dell'inoltro della posta elettronica per una cassetta postale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

L'inoltro della posta elettronica consente di configurare una cassetta postale, affinché i messaggi di posta elettronica inviati da quella cassetta postale vengano inoltrati a un'altra cassetta utente interna o esterna all'organizzazione.


> [!IMPORTANT]
> Se si utilizza Office 365 per le aziende, è necessario configurare l'inoltro della posta elettronica nell'<A href="https://go.microsoft.com/fwlink/p/?linkid=834774">interfaccia di amministrazione di Office 365: Configurare l'inoltro della posta elettronica in Office 365</A>



Se l'organizzazione utilizza un ambiente Exchange locale o ibrido, è necessario ricorrere all'interfaccia di amministrazione di Exchange per creare e gestire cassette postali condivise.

## Configurazione dell'inoltro della posta tramite Interfaccia di amministrazione di Exchange

È possibile utilizzare l'Interfaccia di amministrazione di Exchange (EAC) per configurare l'inoltro di posta elettronica a un singolo destinatario interno o esterno (mediante un contatto di posta elettronica) o a più destinatari (mediante un gruppo di distribuzione).

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere La voce "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco degli utenti delle cassette postali, fare clic o toccare la cassetta postale per cui si desidera configurare l'inoltro della posta, quindi fare clic o toccare su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

4.  Sotto **Flusso di posta**, selezionare **Visualizza dettagli** per visualizzare o modificare le impostazioni di inoltro di posta elettronica.
    
    Da questa pagina è possibile impostare il numero massimo di destinatari ai quali l'utente può inviare un messaggio. Per le organizzazioni Exchange locali, il numero di destinatari è illimitato. Per le organizzazioni Exchange Online, il limite è 500 destinatari.

5.  Selezionare la casella di controllo **Abilita l'inoltro**, quindi fare clic o toccare **Sfoglia**.

6.  Nella pagina **Seleziona destinatario**, selezionare un utente al quale inoltrare tutti i messaggi di posta elettronica. Selezionare la casella di controllo **Recapita messaggio all'indirizzo di inoltro e alla cassetta postale** se si desidera che sia il destinatario che l'indirizzo di posta di inoltro ricevano copie delle e-mail inviate. Fare clic o toccare **OK**, quindi **Salva**.

Se si desidera inoltrare la posta elettronica a un indirizzo esterno all'organizzazione o a più destinatari, è possibile farlo.

  - **Indirizzi esterni**Creare un contatto di posta elettronica e quindi, nella procedura sopra indicata, selezionare il contatto nella pagina **Seleziona destinatario**. Per informazioni su come creare un contatto di posta elettronica, consultare [Gestire i contatti di posta](manage-mail-contacts-exchange-2013-help.md).

  - **Più destinatari**Creare un gruppo di distribuzione, aggiungervi i destinatari e quindi, nella procedura sopra riportata, selezionare il contatto nella pagina **Seleziona destinatario**. Per informazioni su come creare un contatto di posta elettronica, consultare [Creazione e gestione dei gruppi di distribuzione](create-and-manage-distribution-groups-exchange-2013-help.md).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta configurazione dell'inoltro della posta, effettuare una delle seguenti operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic o toccare la cassetta postale per cui è stato configurato l'inoltro della posta, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic o toccare **Funzionalità cassette postali**.

4.  Sotto **Flusso di posta** fare clic o toccare **Visualizza dettagli** per visualizzare le impostazioni di inoltro della posta.

## Informazioni aggiuntive

Questo articolo è rivolto agli amministratori. Se si desidera inoltrare la propria posta elettronica a un altro destinatario, consultare gli argomenti seguenti:

  - [Inoltrare i messaggi a un altro account di posta elettronica](https://go.microsoft.com/fwlink/p/?linkid=510866)

  - [Gestione dei messaggi di posta elettronica mediante le regole](https://go.microsoft.com/fwlink/p/?linkid=510869)

Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).


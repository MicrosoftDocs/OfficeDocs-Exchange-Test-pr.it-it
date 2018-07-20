---
title: 'Cancellazione remota in un cellulare: Exchange 2013 Help'
TOCTitle: Cancellazione remota in un cellulare
ms:assetid: 67ba838e-031d-4a98-b277-170683b6f520
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998614(v=EXCHG.150)
ms:contentKeyID: 52057262
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cancellazione remota in un cellulare

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-06_

Gli utenti possono accedere alle informazioni sensibili dell'azienda ogni giorno dal proprio dispositivo. Se un utente smarrisce il cellulare, i dati in esso contenuti potrebbero essere visualizzati da altre persone. In caso di smarrimento del cellulare, è possibile utilizzare l'interfaccia di amministrazione di Exchange o Exchange Management Shell per cancellare dal telefono tutti i dati aziendali e relativi all'utente.


> [!NOTE]
> In questo argomento viene descritto come utilizzare MicrosoftOutlook Web App per eseguire una cancellazione remota su un telefono. L'utente deve aver eseguito l'accesso a Outlook Web App per eseguire una cancellazione remota.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dispositivi mobili" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - La procedura consente di cancellare tutti i dati sul cellulare, incluse le applicazioni installate, le foto e le informazioni personali.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Utilizzare l'interfaccia di amministrazione di Exchange per cancellare il telefono di un utente

È possibile utilizzare EAC per cancellare il telefono di un utente o per annullare la cancellazione remota non ancora completata.

1.  In EAC, selezionare **Destinatari** \> **Cassette postali**.

2.  Selezionare l'utente e in **Dispositivi mobili**, scegliere **Visualizza dettagli**.

3.  Nella pagina **Dettagli dispositivo mobile**, selezionare il dispositivo mobile smarrito, quindi selezionare **Cancella dati**.

4.  Selezionare **Salva**.

## Utilizzare Shell per cancellare il telefono di un utente

È possibile utilizzare il cmdlet **Clear-MobileDevice** di Shell per cancellare il telefono di un utente.

Il seguente comando consente di cancellare il dispositivo WM\_TonySmith e di inviare un messaggio di conferma all'indirizzo admin@contoso.com.

    Clear-MobileDevice -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"

## Utilizzare Outlook Web App per cancellare il telefono di un utente

Gli utenti possono cancellare il proprio telefono tramite Outlook Web App.

1.  In Outlook Web App, selezionare **Impostazioni \> Telefono \> Dispositivi mobili**.

2.  Selezionare il cellulare.

3.  Fare clic o toccare l'icona **Cancella dispositivo**.

## Come verificare se l'operazione ha avuto esito positivo?

Esistono alcuni modi per verificare se la cancellazione remota sia stata completata.

  - Eseguire il cmdlet **Clear-MobileDevice** con il parametro *–NotificationEmailAddresses* configurato. Verrà inviato un messaggio all'indirizzo di posta elettronica fornito al completamento della cancellazione remota.

  - In EAC, verificare lo stato del dispositivo mobile. Lo stato passerà da **Cancellazione in sospeso** a **Cancellazione completata**.

  - In Outlook Web App, verificare lo stato del dispositivo mobile. Lo stato passerà da **Cancellazione in sospeso** a **Cancellazione completata**.


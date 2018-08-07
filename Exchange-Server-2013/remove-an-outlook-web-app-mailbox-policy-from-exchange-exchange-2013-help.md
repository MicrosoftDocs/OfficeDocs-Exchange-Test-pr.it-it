---
title: 'Rimuove criterio cass. post. Outlook Web App da Exchange: Exchange 2013 Help'
TOCTitle: Rimuovere un criterio cassetta postale di Outlook Web App da Exchange
ms:assetid: edab7bac-b62c-4b82-8f21-dcac77cf0e8f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351239(v=EXCHG.150)
ms:contentKeyID: 50482004
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere un criterio cassetta postale di Outlook Web App da Exchange

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-03-15_

È possibile rimuovere un criterio cassetta postale di MicrosoftOutlook Web App da un'organizzazione Exchange utilizzando EAC o Shell.

Per ulteriori attività di gestione relative ai criteri cassetta postale di Outlook Web App, vedere [Criteri cassetta postale di Outlook Web App](outlook-web-app-mailbox-policies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di Outlook Web App" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per rimuovere un criterio cassetta postale di Outlook Web App

1.  In EAC, fare clic su **Autorizzazioni** \> **Criteri di Outlook Web App**.

2.  Nel riquadro dei risultati, fare clic per selezionare il criterio cassetta postale da rimuovere.

3.  Fare clic sul pulsante **Elimina**.

4.  Nella finestra di conferma, fare clic su **Sì** per rimuovere il criterio cassetta postale, oppure fare clic su **No** per annullare.

## Rimozione di un criterio cassetta postale di Outlook Web App tramite Shell

Con questo esempio viene rimosso un criterio cassetta postale di°Outlook Web App denominato°`Policy1`.

    Remove-OwaMailboxPolicy -Name Policy1 

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Remove-OwaMailboxPolicy](https://technet.microsoft.com/it-it/library/dd298103\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il criterio cassetta postale di Outlook Web App sia stato rimosso correttamente:

  - In EAC, fare clic su **Autorizzazioni** \> **Criteri di Outlook Web App**. Il criterio rimosso non dovrebbe essere più visualizzato nell'elenco.


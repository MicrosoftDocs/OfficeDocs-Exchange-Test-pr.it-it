---
title: 'Abilitare o disabilitare Outlook Voice Access per gli utenti: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare Outlook Voice Access per gli utenti
ms:assetid: c0c244a0-ad2f-4adf-bc1f-1d55fd7ea2d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351106(v=EXCHG.150)
ms:contentKeyID: 52057325
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare Outlook Voice Access per gli utenti

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-12-12_

È possibile abilitare o disabilitare l'accesso ad Outlook Voice Access per gli utenti abilitati alla messaggistica unificata associati a un criterio cassetta postale di messaggistica unificata. Outlook Voice Access è una funzionalità utilizzata dagli utenti abilitati alla messaggistica unificata per accedere alla propria cassetta postale tramite telefono. Questa impostazione è abilitata per impostazione predefinita.

Per ulteriori attività di gestione relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Abilitazione o disabilitazione di Outlook Voice Access tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Sotto **Criteri cassetta postale di messaggistica unificata** selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criteri cassetta postale di messaggistica unificata**, selezionare o deselezionare la casella di controllo accanto a **Consenti Outlook Voice Access**.

4.  Fare clic su **Salva**.

## Abilitazione o disabilitazione di Outlook Voice Access tramite Shell

Con questo esempio si consente agli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy` di utilizzare Outlook Voice Access.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowSubscriberAccess $true

Con questo esempio si impedisce agli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy` di utilizzare Outlook Voice Access.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowSubscriberAccess $false


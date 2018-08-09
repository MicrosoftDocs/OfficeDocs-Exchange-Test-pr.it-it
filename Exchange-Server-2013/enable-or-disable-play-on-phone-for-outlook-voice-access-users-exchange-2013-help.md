---
title: 'Abilita/disab. Ascolta al telefono Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare Ascolta al telefono per gli utenti di Outlook Voice Access
ms:assetid: d3281a97-6fc6-42a3-855f-1af1184a644a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351161(v=EXCHG.150)
ms:contentKeyID: 52057355
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare Ascolta al telefono per gli utenti di Outlook Voice Access

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-12-12_

È possibile abilitare o disabilitare la funzionalità Ascolta al telefono per gli utenti associati a un criterio cassetta postale di messaggistica unificata. Questa opzione è abilitata per impostazione predefinita e consente agli utenti di ascoltare i propri messaggi vocali tramite un apparecchio telefonico. Questa opzione non è disponibile per gli utenti abilitati alla messaggistica unificata che dispongono di una cassetta postale su un server MicrosoftExchange Server 2007.

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

## Abilitazione o disabilitazione di Ascolta al telefono tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio cassetta postale di messaggistica unificata**, selezionare o deselezionare la casella di controllo accanto a **Consenti Ascolta al telefono per la casella vocale**.

4.  Fare clic su **Salva**.

## Abilitazione o disabilitazione di Ascolta al telefono tramite Shell

Con questo esempio viene abilitata la funzionalità Ascolta al telefono per gli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowPlayOnPhone $true

Con questo esempio è possibile disabilitare la funzionalità Ascolta al telefono per gli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowPlayOnPhone $false


---
title: 'Abilita messaggi in attesa indicatore (MWI): Exchange 2013 Help'
TOCTitle: Abilitare i messaggi in attesa indicatore (MWI) per gli utenti
ms:assetid: 3d0ca657-00b6-4108-a850-b092fede1f75
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335216(v=EXCHG.150)
ms:contentKeyID: 50555569
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare i messaggi in attesa indicatore (MWI) per gli utenti

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

È possibile abilitare o disabilitare l'indicatore di messaggio in attesa per gli utenti associati a un criterio cassetta postale di messaggistica unificata. Message Waiting Indicator è una funzionalità di molti sistemi di caselle vocali legacy. Nella modalità più comune, sull'apparecchio telefonico del sottoscrittore si accende una luce che indica la presenza di un nuovo messaggio vocale. L'indicatore di messaggio in attesa può anche inviare un messaggio di testo al cellulare di un utente abilitato alla messaggistica unificata. L'impostazione predefinita è abilitata.

Se l'indicatore di messaggio in attesa è disabilitato sul gateway IP di messaggistica unificata, questa funzionalità non è disponibile per gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata.

Per altre attività di gestione relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Abilitazione dell'indicatore di messaggi in attesa tramite l'interfaccia di amministrazione di Exchange (EAC)

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  In **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio della cassetta postale di messaggistica unificata**, selezionare la casella di controllo accanto a **Consenti l'indicatore di messaggi in attesa**.

4.  Fare clic su **Salva**.

## Abilitazione dell'indicatore di messaggi in attesa tramite Shell

In questo esempio, l'indicatore di messaggi in attesa viene abilitato per gli utenti associati al criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMessageWaitingIndicator $true


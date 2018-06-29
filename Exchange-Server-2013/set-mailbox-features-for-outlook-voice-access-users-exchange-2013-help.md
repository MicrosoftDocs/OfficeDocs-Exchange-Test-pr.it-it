---
title: 'Impostare funzionalità delle cassette postali per gli utenti di Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Impostare funzionalità delle cassette postali per gli utenti di Outlook Voice Access
ms:assetid: 10960bf0-65cf-4d0b-bae5-d203c53662db
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996307(v=EXCHG.150)
ms:contentKeyID: 50555540
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare funzionalità delle cassette postali per gli utenti di Outlook Voice Access

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

Outlook Voice Access contiene due interfacce: l'interfaccia utente telefonica (TUI) e l'interfaccia utente vocale (VUI). È possibile configurare le impostazioni°dell'interfaccia telefonica di un utente abilitato alla messaggistica unificata quando l'utente effettua l'accesso a una cassetta postale utilizzando il sistema Messaggistica unificata di Exchange 2013. Quando si modificano le impostazioni dell'interfaccia telefonica di un utente abilitato alla messaggistica unificata in un criterio cassetta postale di messaggistica unificata, le modifiche vengono applicate a tutti gli utenti associati al criterio cassetta postale di messaggistica unificata. È possibile modificare le seguenti impostazioni dell'interfaccia telefonica per un criterio cassetta postale di messaggistica unificata:

  - Accesso senza PIN alla posta vocale

  - Risposte vocali ad altri messaggi

  - Accesso dell'interfaccia telefonica al calendario

  - Accesso dell'interfaccia telefonica alla directory

  - Accesso dell'interfaccia telefonica alla posta elettronica

  - Accesso dell'interfaccia telefonica ai contatti personali


> [!NOTE]
> Le impostazioni dell'interfaccia telefonica di Outlook&nbsp;Voice Access per gli utenti abilitati alla messaggistica unificata possono essere modificate solo utilizzando Shell.



Per le attività di gestione aggiuntive relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

## Informazioni necessarie prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Modifica delle impostazioni di interfaccia telefonica per un criterio cassetta postale di messaggistica unificata tramite Shell

In questo esempio vengono definite le impostazioni relative all'interfaccia telefonica per il criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Set-UMMailbox -identity MyUMMailboxPolicy -AllowSubscriberAccess $true -AllowTUIAccessToCalendar $false -AllowTUIAccessToDirectory $false -AllowTUIAccessToEmail -$true -AllowTUIAccessToPersonalContacts $true


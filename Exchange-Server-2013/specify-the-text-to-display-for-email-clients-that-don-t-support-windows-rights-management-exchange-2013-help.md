---
title: 'Spec. testo client posta non supp. Windows Rights Management:Exchange 2013 Help'
TOCTitle: Specificare il testo da visualizzare per i client di posta elettronica che non supportano Windows Rights Management
ms:assetid: a9b2238a-b534-469c-a0c3-2768bc3d005b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423552(v=EXCHG.150)
ms:contentKeyID: 52057322
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Specificare il testo da visualizzare per i client di posta elettronica che non supportano Windows Rights Management

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile specificare il testo da inviare a un utente quando riceve un messaggio vocale protetto ma il client di posta elettronica utilizzato non supporta Information Rights Management (IRM) o Windows Rights Management.

È possibile accedere al Sistema di caselle vocali protette solo tramite client di posta elettronica che supportano Windows Rights Management o quando un utente abilitato alla messaggistica unificata utilizza Outlook Voice Access per accedere a un messaggio vocale protetto.

Il Sistema di caselle vocali protette è crittografato. Quando un messaggio vocale è protetto:

  - Il messaggio viene contrassegnato come Privato in Microsoft Outlook e Outlook Web App.

  - Il messaggio vocale può essere aperto solo dal destinatario del messaggio stesso.

  - Il destinatario può rispondere al messaggio vocale ma non può inoltrarlo a utenti non inclusi nel messaggio vocale originale.

Se un messaggio vocale protetto viene inviato a un utente il cui client di posta elettronica non supporta Windows Rights Management e che non accede al messaggio con Outlook Voice Access, l'utente riceverà un messaggio di posta elettronica che include il testo specificato. Tale testo deve comprendere le istruzioni su cosa deve fare la parte chiamata per poter ricevere il messaggio vocale protetto.

Per ulteriori attività di gestione relative alla procedure del Sistema di caselle postali protette, vedere [Procedure della casella vocale protette](protected-voice-mail-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postale di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per specificare il testo da visualizzare per i client di posta elettronica che non supportano Windows Rights Management

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio cassetta postale di messaggistica unificata** \> **Sistema di caselle vocali protette**, sotto **Messaggio per gli utenti senza il supporto di Windows Rights Management**, digitare il testo nella casella di testo.

4.  Fare clic su **Salva**.

## Utilizzo di Shell per specificare il testo da visualizzare per i client di posta elettronica che non supportano Windows Rights Management

In questo esempio viene specificato il testo da visualizzare per gli utenti associati al criterio di cassetta postale di messaggistica unificata `MyUMMailboxPolicy` che utilizzano client di posta elettronica che non supportano Rights Management.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectedVoiceMailText "Your email client software does not support Protected Voice Mail. Please contact the Help Desk."


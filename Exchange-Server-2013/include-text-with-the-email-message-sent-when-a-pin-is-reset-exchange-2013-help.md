---
title: 'Includi testo con il messaggio di posta elettronica inviato quando una reimpostazione pin: Exchange 2013 Help'
TOCTitle: Includi testo con il messaggio di posta elettronica inviato quando una reimpostazione pin
ms:assetid: f7a4d775-a588-412f-ac2c-11ab1a5c67eb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201750(v=EXCHG.150)
ms:contentKeyID: 51407436
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Includi testo con il messaggio di posta elettronica inviato quando una reimpostazione pin

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile immettere testo aggiuntivo nel messaggio di posta elettronica inviato agli utenti quando viene reimpostato il PIN di messaggistica unificata. A tale scopo, immettere il testo personalizzato nella casella **Quando il PIN di Outlook Voice Access di un utente viene reimpostato** in una criterio cassetta postale di messaggistica unificata. Il testo personalizzato può includere, ad esempio, informazioni relative alla protezione per gli utenti abilitati alla messaggistica unificata.

Per impostazione predefinita, un PIN utilizzato per Outlook Voice Access viene reimpostato dalla messaggistica unificata o dal sistema di caselle vocali se vengono eseguiti più di 5 tentativi di accesso non riusciti. Gli utenti possono reimpostare i propri PIN utilizzando le funzionalità di messaggistica unificata incluse in Outlook Web App o Outlook 2010 o versione successiva oppure utilizzando Outlook Voice Access da un telefono.


> [!NOTE]
> Il testo immesso in questa casella è limitato a 512 caratteri e può includere testo HTML semplice.



Per ulteriori attività relative alla protezione del PIN di Outlook Voice Access, vedere [Procedure di protezione PIN](pin-security-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per aggiungere testo al messaggio di posta elettronica inviato agli utenti quando viene reimpostato il PIN

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio cassetta postale di messaggistica unificata** \> **Testo messaggio**, nella casella di testo per **Quando il PIN di Outlook Voice Access di un utente viene reimpostato**, immettere il testo da includere nel messaggio di posta elettronica inviato quando il PIN di in utente viene reimpostato.

4.  Fare clic su **Salva**.

## Utilizzo di Shell per aggiungere testo al messaggio di posta elettronica inviato agli utenti quando viene reimpostato il PIN

In questo esempio viene immesso il testo aggiuntivo, "Non condividere il PIN con altri utenti per non incorrere in azioni disciplinari.", nel messaggio di posta elettronica inviato agli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy` quando viene reimpostato il PIN.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ResetPINText "Do not share your PIN with other users. Doing so may result in disciplinary action."


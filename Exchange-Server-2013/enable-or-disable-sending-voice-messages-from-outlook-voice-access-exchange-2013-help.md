---
title: "Abilitare o disabilitare l'invio di messaggi vocali da Outlook Voice Access: Exchange 2013 Help"
TOCTitle: Abilitare o disabilitare l'invio di messaggi vocali da Outlook Voice Access
ms:assetid: 63544ae2-6a28-40b2-82fc-3df83e93ee56
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423546(v=EXCHG.150)
ms:contentKeyID: 52057257
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare l'invio di messaggi vocali da Outlook Voice Access

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-12-13_

È possibile abilitare gli utenti di Outlook Voice Access per l'invio di messaggi vocali verso altri utenti abilitati alla messaggistica unificata associati allo stesso dial plan oppure impedire loro di eseguire tale operazione.

Questa impostazione è abilitata per impostazione predefinita. Se si disabilita tale impostazione, gli utenti di Outlook Voice Access, che chiamano un numero di Outlook Voice Access, non sono in grado di inviare messaggi vocali agli utenti dello stesso dial plan.

Per altre attività relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare l'interfaccia di amministrazione di Exchange per abilitare gli utenti di Outlook Voice Access o impedire loro l'invio di messaggi vocali verso gli utenti dello stesso dial plan

1.  Nell'interfaccia di amministrazione di Exchange, passare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  In **Trasferisci e cerca**, alla sezione **Consenti ai chiamanti di**, selezionare **Lasciare messaggi vocali senza far squillare il telefono di un utente** per poter inviare i messaggi vocali. Per impedire l'invio di messaggi vocali agli utenti, deselezionare questa impostazione.

5.  Fare clic su **Salva**.

## Utilizzo di Shell per abilitare gli utenti di Outlook Voice Access o impedire loro l'invio di messaggi vocali agli utenti dello stesso dial plan

In questo esempio vengono abilitati gli utenti di Outlook Voice Access associati al dial plan di messaggistica unificata denominato `MyUMDialPlan` a inviare i messaggi vocali agli utenti associati allo stesso dial plan.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $true

In questo esempio viene impedito agli utenti di Outlook Voice Access associati al dial plan di messaggistica unificata denominato `MyUMDialPlan` l'invio di messaggi vocali agli utenti associati allo stesso dial plan.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $false


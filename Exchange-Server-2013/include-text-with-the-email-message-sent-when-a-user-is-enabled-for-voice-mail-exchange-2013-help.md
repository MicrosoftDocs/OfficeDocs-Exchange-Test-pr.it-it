---
title: 'Includi testo con il messaggio di posta elettronica inviato quando un utente è abilitato per la segreteria telefonica: Exchange 2013 Help'
TOCTitle: Includi testo con il messaggio di posta elettronica inviato quando un utente è abilitato per la segreteria telefonica
ms:assetid: 3e8292fb-0cdb-445d-8048-a59af7c38d63
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201679(v=EXCHG.150)
ms:contentKeyID: 51407363
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Includi testo con il messaggio di posta elettronica inviato quando un utente è abilitato per la segreteria telefonica

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-12-16_

Quando la cassetta postale dell'utente viene abilitata alla posta vocale di messaggistica unificata, all'utente della messaggistica unificata viene inviato un messaggio di posta elettronica di benvenuto. Il messaggio contiene il PIN che l'utente dovrà utilizzare per accedere al sistema di posta vocale.

È possibile personalizzare il testo del messaggio di posta elettronica di benvenuto aggiungendo il testo desiderato nella casella **Quando un utente è abilitato alla messaggistica unificata** in un criterio cassetta postale di messaggistica unificata. È possibile specificare informazioni come, ad esempio, i numeri di telefono del supporto tecnico per la messaggistica unificata o i numeri di Outlook Voice Access. Una volta aggiunto, il testo verrà incluso nel messaggio di posta elettronica che sarà inviato ogni volta che un utente associato al criterio cassetta postale di messaggistica unificata viene abilitato alla messaggistica unificata.


> [!NOTE]
> Il testo personalizzato che viene aggiunto al messaggio di benvenuto non deve superare i 512 caratteri.



Per altre attività di gestione relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per personalizzare il testo da inviare quando una cassetta postale viene abilitata alla messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criteri di messaggistica unificata** \> **Testo messaggio**, nella casella di testo **Quando un utente è abilitato alla messaggistica unificata**, inserire il testo che si desidera includere al messaggio di posta elettronica che viene inviato quando un utente è abilitato alla posta vocale della messaggistica unificata.

4.  Fare clic su **Salva**.

## Utilizzo di Shell per personalizzare il testo da inviare quando una cassetta postale viene abilitata alla messaggistica unificata

In questo esempio gli utenti abilitati alla messaggistica unificata e associati a un criterio cassetta postale di messaggistica unificata vengono abilitati a ricevere le altre istruzioni su tale sistema e il numero di Outlook Voice Access utile per accedere alla propria cassetta postale via telefono.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You've been enabled for Unified Messaging voice mail. To access your Exchange mailbox, call your internal telephone extension number. From outside your office, call 425-555-1234."


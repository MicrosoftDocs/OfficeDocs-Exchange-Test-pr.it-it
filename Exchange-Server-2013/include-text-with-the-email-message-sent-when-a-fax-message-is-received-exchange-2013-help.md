---
title: 'Includi testo con il messaggio di posta elettronica inviato quando si riceve un messaggio di fax: Exchange 2013 Help'
TOCTitle: Includi testo con il messaggio di posta elettronica inviato quando si riceve un messaggio di fax
ms:assetid: 48244e58-b7d6-4f0e-bbae-d22bf0fc11ff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201684(v=EXCHG.150)
ms:contentKeyID: 51407357
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Includi testo con il messaggio di posta elettronica inviato quando si riceve un messaggio di fax

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

È possibile includere altro testo nel messaggio di posta elettronica inviato quando un messaggio fax viene ricevuto dagli utenti abilitati alla posta vocale della messaggistica unificata e al fax e quando il criterio cassetta postale di messaggistica unificata è stato configurato correttamente per l'utilizzo di un provider partner fax. Per impostazione predefinita, il testo incluso in questi casi indica solo che l'utente ha ricevuto un messaggio fax. Tuttavia, è possibile creare un messaggio personalizzato aggiungendo del testo nella casella **Quando un utente riceve un messaggio fax** su un criterio cassetta postale di messaggistica unificata. Ad esempio, possono essere incluse informazioni sui criteri di sicurezza del sistema e descrizioni su come gestire correttamente i messaggi fax nell'organizzazione. Una volta aggiunto, il testo verrà incluso in ogni messaggio di posta elettronica inviato quando gli utenti abilitati alla messaggistica unificata e associati al criterio cassetta postale di messaggistica unificata ricevono un messaggio fax.


> [!NOTE]
> Il testo personalizzato che accompagna un messaggio fax non deve superare i 512 caratteri e può includere testo HTML semplice.



Per ulteriori informazioni sui partner fax, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Per altre attività di gestione relative alle operazioni fax, vedere [Fax procedure](faxing-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Modifica del testo incluso in un messaggio fax tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criteri di messaggistica unificata** \> **Testo messaggio**, nella casella di testo **Quando un utente è abilitato alla messaggistica unificata**, inserire il testo che si desidera includere al messaggio di posta elettronica che viene inviato quando un utente è abilitato alla posta vocale della messaggistica unificata.

4.  Fare clic su **Salva**.

## Modifica del testo incluso in un messaggio fax tramite Shell

In questo esempio, gli utenti abilitati alla messaggistica unificata e associati a un criterio cassetta postale di messaggistica unificata vengono abilitati a ricevere ulteriori istruzioni su come aprire un messaggio fax ricevuto sulla cassetta postale.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -FaxMessageText "To open this fax message, double-click the file attachment."


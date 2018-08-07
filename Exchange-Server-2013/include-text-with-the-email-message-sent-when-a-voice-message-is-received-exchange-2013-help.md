---
title: 'Includi testo e mess. inviato se ricevuto mess. vocale: Exchange 2013 Help'
TOCTitle: Includi testo con il messaggio di posta elettronica inviato quando viene ricevuto un messaggio vocale
ms:assetid: b2eec29c-e5eb-4263-80d8-0b9813dd56dc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201718(v=EXCHG.150)
ms:contentKeyID: 51407398
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Includi testo con il messaggio di posta elettronica inviato quando viene ricevuto un messaggio vocale

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-12-16_

È possibile includere testo aggiuntivo nel messaggio di posta elettronica inviato quando un utente abilitato alla posta vocale della messaggistica unificata riceve un messaggio di posta vocale. Per impostazione predefinita, il testo incluso nel messaggio vocale indica solo che l'utente ha ricevuto un messaggio vocale. Tuttavia, è possibile creare un messaggio personalizzato aggiungendo testo nella casella **Quando un utente riceve un messaggio vocale** di un criterio cassetta postale di messaggistica unificata. Ad esempio, possono essere incluse informazioni sui criteri di protezione del sistema e descrizioni su come gestire correttamente i messaggi vocali nella propria organizzazione. Una volta aggiunto, il testo verrà incluso in ogni messaggio di posta elettronica inviato quando gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata ricevono un messaggio vocale.


> [!NOTE]
> Il testo personalizzato che accompagna un messaggio vocale non può superare i 512 caratteri e può includere testo HTML semplice.



Per ulteriori attività di gestione aggiuntive relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Modifica del testo incluso in un messaggio vocale tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio cassetta postale di messaggistica unificata** \> **Testo messaggio**, nella casella di testo per **Quando un utente riceve un messaggio vocale**, immettere il testo da includere nel messaggio di posta elettronica inviato quando gli utenti ricevono un messaggio vocale.

4.  Fare clic su **Salva**.

## Modifica del testo incluso in un messaggio vocale tramite Shell

Con questo esempio viene inserito il testo aggiuntivo "Do not forward voice message to users outside this organization" nei messaggi vocali inviati agli utenti associati al criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailText "Do not forward voice messages to users outside this organization."


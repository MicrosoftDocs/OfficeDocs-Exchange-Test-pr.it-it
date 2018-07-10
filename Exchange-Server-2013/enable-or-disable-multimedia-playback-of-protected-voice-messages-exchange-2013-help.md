---
title: 'Abilitare o disabilitare la riproduzione multimediale dei messaggi vocali protetti: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare la riproduzione multimediale dei messaggi vocali protetti
ms:assetid: 3c33370c-4262-42b1-8d83-d61fc7c426cd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423543(v=EXCHG.150)
ms:contentKeyID: 52057228
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare la riproduzione multimediale dei messaggi vocali protetti

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile spronare gli utenti che ricevono messaggi vocali protetti ad utilizzare la funzionalità Ascolta al telefono per ascoltare i propri messaggi. Oppure, se il software client non supporta la gestione dei diritti, gli utenti devono utilizzare Outlook Voice Access per ascoltare i messaggi.

Per ascoltare i messaggi vocali, gli utenti abilitati alla messaggistica unificata possono utilizzare la funzionalità Ascolta al telefono oppure il software multimediale su computer o dispositivo portatile. La riproduzione multimediale consente agli utenti abilitati alla messaggistica unificata di utilizzare un lettore multimediale sugli altoparlanti del computer o su un cellulare per ascoltare il messaggio vocale.


> [!NOTE]
> Il sistema di caselle vocali protette è disponibile solo su client che utilizzano una versione di Outlook che supporta la gestione dei diritti. Oppure, se il software client non supporta la gestione dei diritti, gli utenti devono utilizzare Outlook Voice Access per ascoltare le chiamate.



Per impostazione predefinita, il valore della proprietà **RequireProtectedPlayOnPhone** in un criterio cassetta postale di messaggistica unificata è impostato su False. Questo significa che gli utenti abilitati alla messaggistica unificata associati ad un criterio cassetta postale di messaggistica unificata, possono ascoltare i messaggi vocali protetti nei seguenti modi:

  - Utilizzando Outlook Voice Access.

  - Utilizzando il lettore multimediale incorporato o il pulsante Ascolta al telefono in Outlook 2010 o versione successiva.

  - Utilizzando il lettore multimediale incorporato o il pulsante Ascolta al telefono in Outlook Web App.

Se questo valore è impostato su True, la riproduzione multimediale dei messaggi vocali protetti non verrà consentita. Gli utenti abilitati alla messaggistica unificata associati a un criterio cassetta postale di messaggistica unificata con il valore impostato su True, possono ascoltare i messaggi vocali protetti solo:

  - Utilizzando Outlook Voice Access.

  - Utilizzando il pulsante Ascolta al telefono in Outlook 2010 o versione successiva.

  - Utilizzando il pulsante Ascolta al telefono in Outlook Web App.

Ciò è particolarmente utile quando gli utenti abilitati alla messaggistica unificata utilizzano computer pubblici, computer portatili in luoghi pubblici o il lettore multimediale del dispositivo mobile per ascoltare la posta vocale protetta contenente informazioni private.

Per le altre attività di gestione relative alle procedure Sistema di posta vocale protetta, vedere [Procedure della casella vocale protette](protected-voice-mail-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare l'interfaccia di amministrazione di Exchange per abilitare o disabilitare la riproduzione multimediale dei messaggi vocali protetti

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  In **Criteri cassetta postale messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio cassetta postale di messaggistica unificata**, \> **Sistema di posta vocale protetta**, selezionare la casella di controllo accanto a **Richiedi Ascolta al telefono per i messaggi vocali protetti** per attivare questa impostazione. Per disattivarla, deselezionare la casella di controllo.

4.  Fare clic su **Salva**.

## Abilitazione o disabilitazione della riproduzione multimediale dei messaggi vocali protetti tramite Shell

In questo esempio, agli utenti associati al criterio cassetta postale di messaggistica unificata denominata `MyUMMailboxPolicy` è consentito di riprodurre messaggi vocali protetti utilizzando un lettore multimediale.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $false

In questo esempio, agli utenti associati al criterio cassetta postale di messaggistica unificata denominata `MyUMMailboxPolicy` non è consentito riprodurre messaggi vocali protetti utilizzando un lettore multimediale.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $true


---
title: 'Consentire o impedire agli utenti gli stessi criteri cassetta postale di messaggistica unificata di creazione di regole di ricezione chiamata: Exchange 2013 Help'
TOCTitle: Consentire o impedire agli utenti gli stessi criteri cassetta postale di messaggistica unificata di creazione di regole di ricezione chiamata
ms:assetid: e44acaa6-d5a8-41e8-94aa-100be0bd6391
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351209(v=EXCHG.150)
ms:contentKeyID: 50555689
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire o impedire agli utenti gli stessi criteri cassetta postale di messaggistica unificata di creazione di regole di ricezione chiamata

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

È possibile consentire agli utenti associati a un criterio cassetta postale di messaggistica unificata di configurare le regole di ricezione chiamata oppure impedire loro questa attività. Se l'opzione per la configurazione delle regole di ricezione chiamata è disabilitata su un dial plan di messaggistica unificata, la funzionalità delle regole di ricezione chiamata non sarà disponibile per gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata. Per impostazione predefinita la funzionalità è abilitata.

Per ulteriori attività di gestione correlate all'abilitazione degli utenti all'inoltro delle chiamate, vedere [Inoltro di chiamate di procedure](forwarding-calls-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per abilitare o disabilitare le regole di ricezione chiamata in un criterio cassetta postale di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Sotto **Criteri cassetta postale di messaggistica unificata** selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio cassetta postale di messaggistica unificata** selezionare o deselezionare la casella di controllo accanto a **Consenti agli utenti di configurare le regole di ricezione chiamata**.

4.  Fare clic su **Salva**.

## Abilitazione o disabilitazione delle regole per il risponditore automatico in un criterio cassetta postale di messaggistica unificata tramite Shell

Con questo esempio viene consentito agli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy` di creare le regole di ricezione chiamata.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $true

Con questo esempio si impedisce agli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy` di creare regole per il risponditore automatico.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $false


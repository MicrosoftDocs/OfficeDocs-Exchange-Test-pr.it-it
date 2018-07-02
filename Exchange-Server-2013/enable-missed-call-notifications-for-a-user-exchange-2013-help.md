---
title: 'Attivare le notifiche di chiamata senza risposta a un utente: Exchange 2013 Help'
TOCTitle: Attivare le notifiche di chiamata senza risposta a un utente
ms:assetid: aa0cbb60-5422-474f-af16-621aade31c1f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232159(v=EXCHG.150)
ms:contentKeyID: 52057309
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attivare le notifiche di chiamata senza risposta a un utente

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-12-09_

È possibile attivare o disattivare le notifiche di chiamata senza risposta per un criterio cassetta postale di messaggistica unificata (UM) utilizzando la Shell o EAC. Una notifica di chiamata senza risposta è un messaggio di posta elettronica inviato a un utente quando l'utente non risponde a una chiamata in arrivo e il chiamante non lascia un messaggio della segreteria telefonica. Si tratta di un messaggio di posta elettronica diverso rispetto al messaggio contenente il messaggio vocale lasciato per un utente.

Se le notifiche di chiamata senza risposta vengono disabilitate in un criterio cassetta postale di messaggistica unificata, gli utenti associati al criterio non riceveranno un messaggio di posta elettronica quando non rispondono a una chiamata in arrivo. Per impostazione predefinita, le notifiche di chiamata senza risposta vengono abilitate per ciascun criterio cassetta postale di messaggistica unificata creato. Per impostazione predefinita, ogni volta che si crea un dial plan di messaggistica unificata viene creato un criterio cassetta postale di messaggistica unificata.


> [!NOTE]
> Quando si esegue l'integrazione tra la messaggistica unificata e Microsoft Lync Server, le notifiche delle chiamate senza risposta non sono disponibili per gli utenti la cui cassetta postale si trova su un server Exchange 2007 o Exchange 2010 quando l'utente si disconnette prima che la chiamata venga inviata a un server Cassette postali su cui è in esecuzione il servizio di messaggistica unificata di Microsoft Exchange.



Per ulteriori attività di gestione relative ai criteri cassetta postale di messaggistica unificata, vedere [Gestire i criteri cassetta postale di messaggistica unificata](manage-a-um-mailbox-policy-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per abilitare o disabilitare le notifiche di chiamata senza risposta per un criterio cassetta postale di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio cassetta postale di messaggistica unificata** \> **Generale**, selezionare la casella di controllo accanto a **Consenti notifiche di chiamata senza risposta**.

4.  Fare clic su **Salva**.

## Utilizzo di Shell per abilitare o disabilitare le notifiche di chiamata senza risposta per un criterio cassetta postale di messaggistica unificata

Con questo esempio vengono abilitate le notifiche di chiamate senza risposta per un criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMissedCallNotifications $true


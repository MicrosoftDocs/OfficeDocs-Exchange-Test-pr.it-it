---
title: 'Elimina criterio cassetta postale mess. unificata: Exchange 2013 Help'
TOCTitle: Eliminare un criterio cassetta postale di messaggistica unificata
ms:assetid: c8758464-3c52-4dd3-b2a6-142a99bb0628
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124536(v=EXCHG.150)
ms:contentKeyID: 50555692
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eliminare un criterio cassetta postale di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-05_

Una volta rimosso, il criterio cassetta postale di messaggistica unificata non potrà più essere associato ai destinatari abilitati alla messaggistica unificata. Non è possibile eliminare un criterio cassetta postale di messaggistica unificata se a esso fanno riferimento cassette postali abilitate alla messaggistica unificata. Non è nemmeno possibile eliminare un dial plan di messaggistica unificata se a esso è associato un criterio cassetta postale di messaggistica unificata.

Per le attività di gestione aggiuntive relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Eliminazione di un criterio cassetta postale di messaggistica unificata tramite EAC

1.  
    
    Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassetta postale di messaggistica unificata**, sulla barra degli strumenti, fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

## Eliminazione di un criterio cassetta postale di messaggistica unificata tramite Shell

Con questo esempio viene eliminato un criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Remove-UMMailboxPolicy -Identity MyUMMailboxPolicy


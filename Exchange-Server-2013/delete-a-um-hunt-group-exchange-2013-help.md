---
title: 'Eliminare un gruppo di risposta di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Eliminare un gruppo di risposta di messaggistica unificata
ms:assetid: 11ac102d-b58d-486c-85b6-e096428e556d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996318(v=EXCHG.150)
ms:contentKeyID: 50555541
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eliminare un gruppo di risposta di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-05_

Una volta eliminato il gruppo di risposta di messaggistica unificata (UM), il gateway IP di messaggistica unificata associato al gruppo di risposta non gestirà né risponderà più alle chiamate in arrivo. Se l'eliminazione del gruppo di risposta di messaggistica unificata lascia il gateway IP di messaggistica unificata senza gruppi di risposta rimanenti configurati, il gateway IP non sarà più in grado di gestire o di elaborare le chiamate di messaggistica unificata.

Per altre attività relative ai dial plan di messaggistica unificata, vedere [Procedure gruppo di risposta di messaggistica unificata](um-hunt-group-procedures-exchange-2013-help.md).


> [!WARNING]
> Per modificare le impostazioni del gruppo di risposta di messaggistica unificata, è necessario eliminare il gruppo di risposta e crearne un altro con le impostazioni corrette.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di risposta di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È indispensabile confermare la creazione di un gateway IP di messaggistica unificata prima di eseguire queste procedure. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - È necessario confermare la creazione del gruppo di risposta di messaggistica unificata prima di eseguire queste procedure. Per la procedura dettagliata, vedere [Creazione di un gruppo di risposta di messaggistica unificata](create-a-um-hunt-group-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Utilizzare EAC per eliminare un gruppo di risposta di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan che si desidera modificare e sulla barra degli strumenti fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Gruppi di risposta di messaggistica unificata**, sulla barra degli strumenti, fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

3.  Nella pagina **Avviso** fare clic su **Sì**.

## Utilizzare Shell per eliminare un gruppo di risposta di messaggistica unificata

In questo esempio viene eliminato un gruppo di risposta di messaggistica unificata denominato `MyUMHuntGroup`.

    Remove-UMHuntGroup -identity MyUMHuntGroup


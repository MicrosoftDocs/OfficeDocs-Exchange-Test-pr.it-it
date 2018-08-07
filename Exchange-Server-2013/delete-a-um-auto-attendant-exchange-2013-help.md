---
title: 'Elimina operatore automatico di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Eliminare un operatore automatico di messaggistica unificata
ms:assetid: 92846bbc-e6b9-45fc-8702-ef5c92eeb08f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123780(v=EXCHG.150)
ms:contentKeyID: 50481184
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eliminare un operatore automatico di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-30_

Una volta eliminato un operatore automatico di messaggistica unificata, le chiamate in arrivo a cui rispondeva l'operatore automatico di messaggistica unificata ricevono risposta da un operatore. Un operatore automatico di messaggistica unificata non può essere eliminato se è associato a un dial plan di messaggistica unificata come operatore automatico di messaggistica unificata predefinito.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare EAC per eliminare un operatore automatico di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata che si desidera eliminare. Fare clic sul pulsante **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina") sulla barra degli strumenti. Nella pagina **Avviso** fare clic su **Sì**.

## Eliminazione di un operatore automatico di messaggistica unificata tramite Shell

Con questo esempio viene eliminato un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant`.

    Remove-UMAutoAttendant -Identity MyUMAutoAttendant


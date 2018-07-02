---
title: 'Disabilitare un operatore automatico di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Disabilitare un operatore automatico di messaggistica unificata
ms:assetid: ad79f374-f68f-430b-8b9c-2c841e1c55ae
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124228(v=EXCHG.150)
ms:contentKeyID: 50481409
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare un operatore automatico di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-05_

Per impostazione predefinita, quando viene creato un operatore automatico di messaggistica unificata (UM), il relativo stato è impostato su disabilitato. Dopo aver creato l'operatore automatico di messaggistica unificata, è possibile modificare lo stato per controllare se è possibile rispondere alle chiamate in arrivo. Ad esempio, è possibile disabilitare l'operatore automatico di messaggistica unificata quando si sta registrando o ripetere la registrazione delle istruzioni personalizzate e i messaggi.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per ulteriori informazioni, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md). Verificare inoltre che lo stato dell'operatore automatico di messaggistica unificata è impostato su abilitato.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare EAC per disabilitare un operatore automatico di messaggistica unificata

1.  In EAC, accedere a **Messaggistica unificata** \> **dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan che si desidera modificare e sulla barra degli strumenti, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial Plan**, in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata da disattivare. Sulla barra degli strumenti, fare clic **sulla freccia in giù**![Icona Freccia in giù](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icona Freccia in giù")

3.  Nella pagina **Avviso** fare clic su **Sì**.

## Utilizzo della Shell per disabilitare un operatore automatico di messaggistica unificata

In questo esempio consente di disabilitare un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant`.

    Disable-UMAutoAttendant -Identity MyUMAutoAttendant


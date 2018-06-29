---
title: 'Configurare il fuso orario: Exchange 2013 Help'
TOCTitle: Configurare il fuso orario
ms:assetid: 30d769e1-3657-4622-bc9a-643c63cf46d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997162(v=EXCHG.150)
ms:contentKeyID: 50555562
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il fuso orario

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-17_

Per impostazione predefinita, l'operatore automatico di messaggistica unificata utilizza il fuso orario del server Cassette postali su cui viene creato. Tuttavia, in alcuni casi è possibile cambiare il fuso orario dell'operatore automatico di messaggistica unificata. Ad esempio, in presenza di due dial plan di messaggistica unificata in cui ciascuno rappresenta un diverso fuso orario, è necessario configurare un operatore automatico di messaggistica unificata in modo che abbia lo stesso fuso orario del server Cassette postali e l'altro operatore in modo che abbia un fuso orario diverso da quello del server Cassette postali.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Configurazione del fuso orario tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per il quale si desidera impostare il fuso orario, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata**, fare clic su **Orario di ufficio** e quindi, sotto **Fuso orario**, selezionare il fuso orario desiderato nell'elenco a discesa.

4.  Per salvare le modifiche, fare clic su **OK** e quindi su **Salva**.

## Configurazione del fuso orario tramite Shell

In questo esempio viene configurato il fuso orario del Pacifico su un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -TimeZoneName Pacific


---
title: 'Configurare il limite nel messaggio di saluto personale per gli utenti di Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurare il limite nel messaggio di saluto personale per gli utenti di Outlook Voice Access
ms:assetid: d400f250-0f55-45f5-9918-5f1d7819fbdf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201731(v=EXCHG.150)
ms:contentKeyID: 50555687
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il limite nel messaggio di saluto personale per gli utenti di Outlook Voice Access

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-05_

The L'impostazione **Limite per i messaggi di saluto personali (minuti)** consente di immettere il numero massimo di minuti a disposizione degli utenti associati ai criteri cassetta postale di messaggistica unificata per la registrazione di messaggi di saluto del sistema di caselle vocali. Questa impostazione si applica ai messaggi di saluto standard e Fuori sede del sistema di caselle vocali. Per impostazione predefinita, la durata massima del messaggio di saluto è 5 minuti. Tuttavia, è possibile impostare la durata massima del messaggio di saluto su qualsiasi valore compreso tra 1 e 10 minuti.

Per le attività di gestione aggiuntive relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Modifica della durata massima del messaggio di saluto tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare e sulla barra degli strumenti fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi sulla barra degli strumenti fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criteri cassetta postale di messaggistica unificata** \> **Generali**, sotto **Limite per i messaggi di saluto personali (minuti)**, immettere l'arco di tempo in minuti consentito per registrare i messaggi di saluto personali agli utenti delle caselle vocali.

4.  Fare clic su **Salva**.

## Modifica della durata massima del messaggio di saluto tramite Shell

Con questo esempio viene configurata su 3 minuti la durata massima del messaggio di saluto per il criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy MaxGreetingDuration 3


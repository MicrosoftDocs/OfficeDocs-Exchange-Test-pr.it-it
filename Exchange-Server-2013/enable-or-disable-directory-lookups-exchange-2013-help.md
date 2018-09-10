---
title: 'Abilitare o disabilitare le ricerche di directory: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare le ricerche di directory
ms:assetid: c0768815-8578-4385-8d4c-7d1e40304cec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423557(v=EXCHG.150)
ms:contentKeyID: 52057324
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare le ricerche di directory

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-05-10_

È possibile abilitare le ricerche nelle directory in modo che i chiamati che chiamano un operatore automatico di messaggistica unificata possa cercare i nomi nella directory utilizzando il tastierino telefonico ma non tramite input vocali. Questa impostazione è abilitata per impostazione predefinita. Se questa impostazione viene disabilitata, i chiamanti non riusciranno a cercare nella directory una specifica persona utilizzando la composizione a toni o i comandi vocali.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).


> [!NOTE]
> Outlook Voice Access è possibile utilizzare il riconoscimento vocale automatico (ASR) o gli input vocali per collocare gli utenti nella directory, è possibile utilizzare solo DTMF o gli input di composizione a toni.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Abilitazione o disabilitazione delle ricerche nella directory tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per il quale si desidera abilitare o disabilitare le ricerche nelle directory, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata** \> **Accesso operatore e rubrica**, sotto **Opzioni per la ricerca nella rubrica**, selezionare la casella di controllo accanto a **Consenti ai chiamanti di cercare un utente per nome o alias** per consentire ai chiamati di cercare gli utenti. Per impedire ai chiamanti di cercare gli utenti, deselezionare questa casella di controllo.

4.  Fare clic su **Salva**.

## Abilitazione o disabilitazione delle ricerche nella directory tramite Shell

Con questo esempio vengono disabilitate le ricerche nella directory per un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -NameLookupEnabled $false


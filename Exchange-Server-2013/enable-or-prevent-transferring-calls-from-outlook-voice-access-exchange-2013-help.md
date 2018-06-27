---
title: 'Consentire o impedire il trasferimento di chiamate da Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Consentire o impedire il trasferimento di chiamate da Outlook Voice Access
ms:assetid: b80c57f1-394c-4608-8ad3-52a3e6d697db
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423554(v=EXCHG.150)
ms:contentKeyID: 52057321
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire o impedire il trasferimento di chiamate da Outlook Voice Access

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

È possibile consentire o impedire agli utenti di Outlook Voice Access di trasferire le chiamate a un utente associato a un dial plan di messaggistica unificata. Per impostazione predefinita questa opzione e l'opzione **Consenti ai chiamanti di lasciare messaggi vocali senza far squillare il telefono dell'utente** sono abilitate, pertanto gli utenti di Outlook Voice Access possono trasferire le chiamate agli utenti nello stesso dial plan di messaggistica unificata e lasciare messaggi per loro. Questa impostazione si applica solo agli utenti di Outlook Voice Access che hanno inserito il PIN e sono stati autenticati.

Per altre attività relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per consentire o impedire agli utenti di Outlook Voice Access di trasferire le chiamate

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Nuovo dial plan di messaggistica unificata** fare clic su **Configura**.

3.  In **trasferisci & cerca** , sotto **Consenti ai chiamanti**, selezionare la casella di controllo accanto a **trasferimento agli utenti** per consentire ai chiamanti di trasferire le chiamate ad altri utenti nel dial plan. Per impedire agli utenti di Outlook Voice Access di trasferire le chiamate agli utenti, deselezionare la casella di controllo.

4.  Fare clic su **Salva**.

## Utilizzo di Shell per consentire o impedire agli utenti di Outlook Voice Access di trasferire le chiamate

In questo esempio agli utenti di Outlook Voice Access viene consentito di trasferire le chiamate agli utenti nello stesso dial pian in un dial plan di messaggistica unificata denominato `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $true

In questo esempio agli utenti di Outlook Voice Access viene impedito di trasferire le chiamate agli utenti nello stesso dial pian in un dial plan di messaggistica unificata denominato `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $false


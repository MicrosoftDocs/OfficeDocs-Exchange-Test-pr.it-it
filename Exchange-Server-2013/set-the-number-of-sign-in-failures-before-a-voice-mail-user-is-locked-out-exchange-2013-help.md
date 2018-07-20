---
title: 'Impostare il numero di errori di accesso prima che venga bloccato un utente di posta vocale: Exchange 2013 Help'
TOCTitle: Impostare il numero di errori di accesso prima che venga bloccato un utente di posta vocale
ms:assetid: 855e1980-2868-4983-b097-0b5f63f202b8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123544(v=EXCHG.150)
ms:contentKeyID: 50555632
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare il numero di errori di accesso prima che venga bloccato un utente di posta vocale

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile configurare il numero di tentativi di accesso non riusciti prima che agli utenti di Outlook Voice Access non venga più consentito l'accesso alle proprie cassette postali. Il numero di tentativi di accesso non riusciti consentiti prima che una cassetta postale venga bloccata è configurato in un criterio cassetta postale di messaggistica unificata e si applica a tutti gli utenti abilitati alla messaggistica unificata associati a tale criterio. L'impostazione predefinita è 15.

Per aumentare la protezione, diminuire il numero massimo di tentativi non riusciti. Tuttavia, tenere presente che se viene impostato un numero notevolmente inferiore a quello predefinito, l'accesso degli utenti potrebbe essere bloccato senza motivo. La messaggistica unificata genera eventi di avviso che possono essere visualizzati con il Visualizzatore eventi in caso di mancata autenticazione del PIN di un utente abilitato alla messaggistica unificata oppure nel caso di un tentativo di accesso al sistema non riuscito da parte dell'utente. Questa impostazione deve essere superiore all'impostazione stabilita per il numero di tentativi di accesso non riusciti prima che il PIN venga reimpostato.

Per altre attività relative alla protezione tramite PIN di Outlook Voice Access, vedere [Procedure di protezione PIN](pin-security-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Configurazione tramite l'interfaccia di amministrazione di Exchange del numero di tentativi di accesso non riusciti prima che l'utente di una casella vocale venga bloccato

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassette postali di messaggistica unificata** selezionare il criterio cassetta postale di messaggistica unificata da modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Fare clic su **Criteri PIN** e accanto a **Numero di errori accesso prima del blocco** immettere un valore compreso tra 1 e 999.

5.  Fare clic su **Salva**.

## Configurazione tramite Shell del numero di tentativi di accesso non riusciti prima che l'utente di una casella vocale venga bloccato

In questo esempio, il numero massimo di tentativi di accesso è impostato su 10 per gli utenti abilitati alla messaggistica unificata associati a un criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MaxLogonAttempts 10

In questo esempio, per gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`, il numero di tentativi di accesso non riusciti consentiti prima della reimpostazione del PIN utente di Outlook Voice Access viene reimpostato su 3, il numero massimo di tentativi di accesso su 5 e la lunghezza minima del PIN su 9.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9


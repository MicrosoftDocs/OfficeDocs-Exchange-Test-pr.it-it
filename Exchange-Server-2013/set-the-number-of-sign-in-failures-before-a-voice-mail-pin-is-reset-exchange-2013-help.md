---
title: 'Impostare il numero di errori di accesso prima di una segreteria telefonica che è reimpostazione del PIN: Exchange 2013 Help'
TOCTitle: Impostare il numero di errori di accesso prima di una segreteria telefonica che è reimpostazione del PIN
ms:assetid: 4de38499-0a6f-4f00-8697-eeff805d7266
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997939(v=EXCHG.150)
ms:contentKeyID: 50555585
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare il numero di errori di accesso prima di una segreteria telefonica che è reimpostazione del PIN

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile configurare su un intervallo di valori compreso tra 1 e 998 il numero di tentativi di accesso consentiti prima che il PIN venga reimpostato per un utente di Outlook Voice Access. L'impostazione predefinita è 5. Il numero di tentativi di accesso consentiti prima che il PIN venga reimpostato viene configurato nel criterio cassetta postale di messaggistica unificata e applicato a tutti gli utenti di Outlook Voice Access associati a tale criterio.


> [!NOTE]
> La sicurezza può essere rafforzata impostando <STRONG>Numero di errori di accesso prima della reimpostazione del PIN</STRONG> su un numero minore di 5 e diminuita impostando questa opzione su un numero maggiore di 5.



Per altre attività relative al PIN di Outlook Voice Access, vedere [Procedure di protezione PIN](pin-security-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per la configurazione del numero di tentativi di accesso consentiti prima che un PIN venga reimpostato

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio che si desidera modificare e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Fare clic su **Criteri PIN** e quindi immettere un valore compreso tra 0 e 999 in **Numero di errori di accesso prima della reimpostazione del PIN**.

5.  Fare clic su **Salva**.

## Utilizzo di Shell per la configurazione del numero di tentativi di accesso consentiti prima che un PIN venga reimpostato

In questo esempio, il numero massimo di tentativi di accesso prima della reimpostazione del PIN viene reimpostato su 3 per gli utenti abilitati alla messaggistica unificata che sono associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3

In questo esempio, per gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy`, il numero massimo di tentativi di accesso prima della reimpostazione del PIN viene reimpostato su 3, il numero massimo di tentativi di accesso su 5 e la lunghezza minima del PIN su 9.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MaxLogonAttempts 5 -MinPINLength 9


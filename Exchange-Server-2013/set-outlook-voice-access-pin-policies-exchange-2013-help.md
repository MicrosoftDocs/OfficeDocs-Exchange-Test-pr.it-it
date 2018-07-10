---
title: 'Impostare i criteri PIN di Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Impostare i criteri PIN di Outlook Voice Access
ms:assetid: 5b2800b7-bfa6-4282-975c-0706ae25ad64
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998285(v=EXCHG.150)
ms:contentKeyID: 50555593
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare i criteri PIN di Outlook Voice Access

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile impostare i criteri PIN su un criterio cassetta postale di messaggistica unificata. I criteri cassetta postale di messaggistica unificata possono essere configurati in modo da aumentare il livello di sicurezza degli utenti abilitati alla messaggistica unificata che utilizzano Outlook Voice Access chiedendo loro di adeguarsi ai criteri PIN predefiniti dell'organizzazione.

Per impostare i criteri PIN per gli utenti di Outlook Voice Access, è possibile creare un nuovo criterio cassetta postale di messaggistica unificata o modificarne uno esistente. Una volta creato un nuovo criterio cassetta postale di messaggistica unificata, è possibile configurarlo con le seguenti impostazioni del PIN:

  - `MinPasswordLength`

  - `PINLifetime`

  - `LogonFailuresBeforePINReset`

  - `MaxLogonAttempts`

  - `AllowCommonPatterns`

  - `PINHistoryCount`

Per una maggiore sicurezza, si consiglia di implementare requisiti del PIN complessi per gli utenti di messaggistica unificata. Ciò può essere applicato creando criteri PIN di messaggistica unificata che richiedono 6 o più cifre per i PIN, aumentando in tal modo il livello di sicurezza della rete.

Quando si modifica il criterio PIN, la nuova impostazione del PIN viene applicata agli utenti attualmente associati al criterio cassetta postale di messaggistica unificata. Ad esempio, se si modifica il criterio cassetta postale di messaggistica unificata e la lunghezza minima del PIN viene portata da 7 a 10 cifre, al successivo accesso gli utenti saranno obbligati a modificare il proprio PIN per adeguarsi ai requisiti del PIN modificato.

Per le altre attività relative alla sicurezza per il PIN di Outlook Voice Access, vedere [Procedure di protezione PIN](pin-security-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Impostazione dei criteri PIN per gli utenti di Outlook Voice Access tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, fare clic sul dial plan di messaggistica unificata che si intende modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata da modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Fare clic su **Proprietà**.

4.  Nella pagina **Criterio cassetta postale di messaggistica unificata**, fare clic su **Criteri PIN**.

5.  Nella pagina **Criteri PIN**, configurare le impostazioni del PIN per gli utenti di Outlook Voice Access associati a questo criterio cassetta postale di messaggistica unificata, quindi fare clic su **Salva**.

## Impostazione dei criteri PIN per gli utenti di Outlook Voice Access tramite Shell

In questo esempio vengono definite le impostazioni del PIN per gli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."


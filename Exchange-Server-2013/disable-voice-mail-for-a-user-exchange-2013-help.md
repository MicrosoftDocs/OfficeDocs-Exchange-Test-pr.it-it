---
title: 'Disabilitare la segreteria telefonica di un utente: Exchange 2013 Help'
TOCTitle: Disabilitare la segreteria telefonica di un utente
ms:assetid: cecc9c0d-377d-489e-9db4-d487e9c0b552
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124691(v=EXCHG.150)
ms:contentKeyID: 50481732
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare la segreteria telefonica di un utente

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-05_

È possibile disabilitare la messaggistica unificata per un utente abilitato alla messaggistica unificata. A tale scopo, l'utente non è più possibile utilizzare le funzionalità posta vocale di messaggistica unificata. Se si preferisce, quando si disabilita messaggistica unificata per un utente, è possibile mantenere le impostazioni di messaggistica unificata per l'utente.

Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che l'utente esistente sia abilitato alla Messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Disabilitazione della messaggistica unificata e della casella vocale per un utente tramite EAC

1.  In Stima al completamento fare clic su **Destinatari**.

2.  Nella visualizzazione Elenco selezionare l'utente di cui si desidera disabilitare la cassetta postale per la messaggistica unificata.

3.  Nel riquadro dei dettagli, sotto **Funzionalità telefoniche e vocali** \> **Messaggistica unificata** fare clic su **Disabilita** .

4.  Nella finestra di dialogo **Avviso** fare clic su **Sì** per confermare che la messaggistica unificata verrà disabilitata per l'utente.

## Disabilitazione della messaggistica unificata e della casella vocale per un utente tramite Shell

Con questo esempio vengono disabilitate la messaggistica unificata e la casella vocale per l'utente tonysmith@contoso.com, ma le impostazioni della cassetta postale vengono conservate.

    Disable-UMMailbox -Identity tonysmith@contoso.com -KeepProperties $True


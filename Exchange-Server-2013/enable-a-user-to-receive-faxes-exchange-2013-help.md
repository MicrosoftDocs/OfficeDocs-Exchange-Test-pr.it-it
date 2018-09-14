---
title: 'Consentire agli utenti di ricevere fax: Exchange 2013 Help'
TOCTitle: Consentire agli utenti di ricevere fax
ms:assetid: a0505001-aac0-41ef-824f-76e5e56d7675
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201712(v=EXCHG.150)
ms:contentKeyID: 52057308
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire agli utenti di ricevere fax

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile abilitare un utente di messaggistica unificata alla ricezione di fax. Per impostazione predefinita, quando si abilita un utente alla messaggistica unificata, questi sarà in grado di ricevere fax se si consente la ricezione e l'invio di fax e si configura l'URI di un partner fax sul criterio di messaggistica unificata collegato all'utente. L'invio di fax può essere abilitato o disabilitato nei dial plan di messaggistica unificata, nei criteri cassetta postale di messaggistica unificata o nella cassetta postale dell'utente abilitato alla messaggistica unificata.

Per impostazione predefinita, la cassetta postale dell'utente e il dial plan a esso collegato consentono la ricezione di fax in ingresso. Tuttavia, affinché un utente possa ricevere fax, per prima cosa è necessario abilitare la ricezione di fax nei criteri cassetta postale di messaggistica unificata associati all'utente abilitato alla messaggistica unificata e immettere l'URI del partner fax.


> [!NOTE]
> È possibile utilizzare EAC per configurare impostazioni fax su un criterio cassetta postale di messaggistica unificata. Tuttavia, è necessario utilizzare Shell per configurare le impostazioni fax su dial plan o per utenti singoli.



Per ulteriori informazioni sui partner fax, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Per altre attività di gestione relative all'invio e alla ricezione di fax, vedere [Fax procedure](faxing-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, confermare che il criterio di cassetta postale di messaggistica unificata assegnato all'utente sia abilitato alla ricezione e all'invio di fax e che l'URI del partner fax sia correttamente configurato.

  - Prima di eseguire queste procedure, verificare che l'utente sia abilitato alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Abilitazione di un utente di messaggistica unificata alla ricezione di fax tramite Shell

Con questo esempio Tony Smith viene abilitato alla ricezione dei fax in ingresso.

    Set-UMMailbox -Identity tonysmith@contoso.com -FaxEnabled $true


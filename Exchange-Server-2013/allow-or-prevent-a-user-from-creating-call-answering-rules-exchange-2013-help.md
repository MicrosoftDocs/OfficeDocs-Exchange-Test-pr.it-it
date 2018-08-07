---
title: 'Consente o meno di creare regole di ricezione chiamata: Exchange 2013 Help'
TOCTitle: Consentire o impedire a un utente di creare regole di ricezione chiamata
ms:assetid: 81863440-8b21-4523-bdab-6a2311889a0d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298097(v=EXCHG.150)
ms:contentKeyID: 50555628
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire o impedire a un utente di creare regole di ricezione chiamata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile specificare se si desidera consentire a singoli utenti di creare e gestire le proprie regole ricezione chiamata configurando le proprietà delle relative cassette postali. Per impostazione predefinita, possono creare regole di ricezione chiamata.

È possibile abilitare o disabilitare le regole di ricezione chiamata per più utenti abilitati alla messaggistica unificata configurando tali regole su un dial plan di messaggistica unificata o un criterio cassetta postale di messaggistica unificata.


> [!NOTE]
> Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per configurare questa funzionalità. Per abilitare o disabilitare le regole di ricezione chiamata per un utente di posta vocale, è necessario utilizzare Shell.



Per ulteriori attività di gestione per consentire agli utenti di inoltrare chiamate, vedere [Inoltro di chiamate di procedure](forwarding-calls-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Abilitazione o disabilitazione delle regole ricezione chiamata per un utente abilitato alla messaggistica unificata tramite Shell

Con questo esempio vengono abilitate le regole di ricezione chiamata per l'utente tony@contoso.com.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $true

In questo esempio, vengono disabilitate le regole ricezione chiamata per l'utente tony@contoso.com.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $false


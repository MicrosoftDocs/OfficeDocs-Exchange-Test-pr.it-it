---
title: 'Impedire a un utente di ricevere fax: Exchange 2013 Help'
TOCTitle: Impedire a un utente di ricevere fax
ms:assetid: b5d022b9-043a-4324-87fb-074d5e2c2ca3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201722(v=EXCHG.150)
ms:contentKeyID: 52057317
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impedire a un utente di ricevere fax

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Impedire la ricezione dei fax di un utente di messaggistica unificata (UM). Informazioni su come modificare le impostazioni dei fax per gli utenti di messaggistica UNIFICATA nuovi ed esistenti.

Per impostazione predefinita, quando si attiva un utente per la messaggistica unificata, saranno in grado di ricevere fax se si attiva fax e configurare il criterio cassetta postale di messaggistica UNIFICATA che l'utente è collegato URI del partner fax. Fax può essere abilitato o disabilitato nella messaggistica UNIFICATA dial plan, criteri cassetta postale di messaggistica UNIFICATA o cassetta postale dell'utente abilitato alla messaggistica UNIFICATA.

Per impostazione predefinita, la cassetta postale dell'utente e il dial plan collegato all'utente consentono i fax in ingresso. Tuttavia, perché un utente possa ricevere fax è necessario prima abilitare i fax in ingresso nel criterio cassetta postale di messaggistica unificata associato all'utente abilitato alla messaggistica unificata e immettere l'URI del partner fax.


> [!NOTE]
> È possibile utilizzare EAC per configurare le impostazioni fax in un criterio cassetta postale di messaggistica unificata. Tuttavia, è necessario utilizzare la Shell per configurare le impostazioni di fax sul dial plan o per i singoli utenti.



Per ulteriori informazioni sui partner fax, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Per ulteriori attività di gestione relative all'invio e ricezione di fax, vedere [Fax procedure](faxing-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che l'utente sia abilitato alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo della Shell per impedire la ricezione dei fax di un utente abilitato alla messaggistica UNIFICATA

Con questo esempio è possibile impedire a un utente abilitato alla messaggistica unificata chiamato Tony di ricevere messaggi fax nella sua cassetta postale.

    Set-UMMailbox -Identity tony@contoso.com -FaxEnabled $false


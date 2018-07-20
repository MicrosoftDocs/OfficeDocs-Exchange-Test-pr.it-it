---
title: 'Rimuovere una regola di ricezione chiamata di un utente: Exchange 2013 Help'
TOCTitle: Rimuovere una regola di ricezione chiamata di un utente
ms:assetid: 1da3c5bc-7227-4b37-96f6-67ceefc084d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898497(v=EXCHG.150)
ms:contentKeyID: 51407346
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere una regola di ricezione chiamata di un utente

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile utilizzare la Shell per rimuovere uno o più regole di ricezione per un utente di chiamata. È anche possibile utilizzare il cmdlet **Remove-UMCallAnsweringRule** in uno script di Exchange Management Shell per rimuovere uno o più regole di ricezione per più utenti di chiamata.

Le regole di ricezione chiamata vengono applicate alle chiamate in ingresso in modo simile a quello in cui le Regole posta in arrivo vengono applicate ai messaggi di posta in arrivo. Per impostazione predefinita, quando un utente viene abilitato all'utilizzo della messaggistica unificata non viene configurata alcuna regola di ricezione chiamata. Ciononostante, il sistema di posta risponde alle chiamate e ai chiamanti viene chiesto di lasciare un messaggio vocale.


> [!NOTE]
> Gli utenti abilitati alla messaggistica unificata possono accedere a Outlook Web App per creare, gestire e rimuovere regole di ricezione chiamata.



Per ulteriori attività di gestione relative alle regole di ricezione chiamata, vedere [Inoltro di chiamate di procedure](forwarding-calls-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Regole di ricezione chiamata di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)). Per informazioni su come usare Windows PowerShell per connettersi a Exchange Online, vedere [Connessione a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo della Shell per rimuovere una regola di ricezione chiamata

In questo esempio viene rimossa di regola ricezione chiamata `MyUMCallAnsweringRule` dalla cassetta postale dell'utente. Cassetta postale dell'utente è la cassetta postale dell'utente che esegue il cmdlet.

    Remove-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

In questo esempio viene rimossa di regola ricezione chiamata `MyUMCallAnsweringRule` dalla cassetta postale di Tony Smith.

    Remove-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith


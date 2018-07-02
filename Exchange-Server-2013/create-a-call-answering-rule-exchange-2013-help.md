---
title: 'Creare una regola di ricezione chiamata: Exchange 2013 Help'
TOCTitle: Creare una regola di ricezione chiamata
ms:assetid: 0976f8f2-3449-44f1-b0d1-20c91622e827
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898495(v=EXCHG.150)
ms:contentKeyID: 51407336
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare una regola di ricezione chiamata

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile utilizzare la Shell per creare uno o più regole di ricezione per un utente di chiamata. È inoltre possibile utilizzare il cmdlet **New-UMCallAnsweringRule** in uno script di Exchange Management Shell per creare regole di ricezione chiamata per più utenti.

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



## Utilizzo della Shell per creare una regola di ricezione chiamata

Questo esempio viene creato di regola ricezione chiamata `MyCallAnsweringRule` nella cassetta postale di Tony Smith con priorità 2.

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith

In questo esempio viene creata di regola ricezione chiamata `MyCallAnsweringRule` nella cassetta postale di Tony Smith ed esegue le operazioni seguenti:

  - La regola di ricezione chiamata viene impostata su due ID chiamante.

  - La priorità della regola di ricezione chiamata viene impostata su 2.

  - La regola di ricezione chiamata viene impostata per consentire ai chiamanti di interrompere il messaggio di saluto.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

In questo esempio viene creata di regola ricezione chiamata `MyCallAnsweringRule` nella cassetta postale di Tony Smith ed esegue le operazioni seguenti:

  -  
    La priorità della regola di ricezione chiamata viene impostata su 2.

  -  
    Crea il mapping dei tasti per la regola di ricezione chiamata.

  -  
    Se il chiamante raggiunge la segreteria telefonica dell'utente e lo stato dell'utente è Non disponibile, il chiamante può:
    
      - Premere il tasto 1 per essere trasferito a un operatore all'interno 45678.
    
      - Premere il tasto 2 in modo che trova Me funzionalità verrà utilizzato per questioni urgenti, chiamare prima l'interno 23456 e poi passate estensione 45671.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith -ScheduleStatus 0x4 - -KeyMappings "1,1,Receptionist,,,,,45678,","5,2,Urgent Issues,23456,23,45671,50,,"


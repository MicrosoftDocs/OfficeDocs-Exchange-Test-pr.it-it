---
title: 'Visualizzare e gestire una regola di ricezione chiamata: Exchange 2013 Help'
TOCTitle: Visualizzare e gestire una regola di ricezione chiamata
ms:assetid: de6d9fa1-7878-49a9-bddb-e3317d94f4d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn140251(v=EXCHG.150)
ms:contentKeyID: 54652854
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzare e gestire una regola di ricezione chiamata

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile utilizzare Shell per visualizzare o configurare una o più regole di ricezione chiamata per un utente. È possibile, inoltre, utilizzare i cmdlet **Get-UMCallAnsweringRule** o **Set-UMCallAnsweringRule** in uno script di Exchange Management Shell per visualizzare o gestire le regole di ricezione chiamata per più utenti.

Le regole di ricezione chiamata vengono applicate alle chiamate in ingresso in modo simile a quello in cui le Regole posta in arrivo vengono applicate ai messaggi di posta in arrivo. Per impostazione predefinita, quando un utente viene abilitato all'utilizzo della messaggistica unificata non viene configurata alcuna regola di ricezione chiamata. Ciononostante, il sistema di posta risponde alle chiamate e ai chiamanti viene chiesto di lasciare un messaggio vocale.


> [!IMPORTANT]
> Gli utenti abilitati alla messaggistica unificata possono accedere a Outlook Web App per creare, gestire e rimuovere regole di ricezione chiamata.



Per ulteriori attività di gestione relative alle regole di ricezione chiamata, vedere [Inoltro di chiamate di procedure](forwarding-calls-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Regole ricezione chiamata di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)). Per informazioni su come usare Windows PowerShell per connettersi a Exchange Online, vedere [Connessione a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Visualizzazione di una regola di ricezione chiamata tramite Shell

È possibile recuperare le proprietà di una singola regola o di un elenco di regole di ricezione chiamata in una cassetta postale dell'utente abilitato alla messaggistica unificata.

In questo esempio viene restituito un elenco formattato di regole di ricezione chiamata nella cassetta postale abilitata alla messaggistica unificata di un utente.

    Get-UMCallAnsweringRule-Mailbox tonysmith | Format-List

In questo esempio vengono visualizzate le proprietà della regola di ricezione chiamata `MyUMCallAnsweringRule`.

    Get-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

## Configurazione di una regola di ricezione chiamata tramite Shell

È possibile configurare o modificare una regola di ricezione chiamata archiviata nella cassetta postale di un utente. È possibile specificare le seguenti condizioni:

  - Chiamante

  - Ora del giorno

  - Stato della disponibilità calendario

  - Attivazione delle risposte automatiche per i messaggi di posta elettronica

È inoltre possibile specificare le seguenti azioni:

  - Numeri alternativi

  - Trasferimento del chiamante a un altro utente

  - Registrazione di un messaggio vocale

In questo esempio viene impostata la priorità 2 per la regola di ricezione chiamata `MyCallAnsweringRule` esistente nella cassetta postale di Tony Smith.

    Set-UMCallAnsweringRule -Mailbox tonysmith -Name MyCallAnsweringRule -Priority 2

In questo esempio vengono effettuate le seguenti azioni sulla regola di ricezione chiamata `MyCallAnsweringRule` nella cassetta postale di Tony Smith:

  - La regola di ricezione chiamata viene impostata su due ID chiamante.

  - La priorità della regola di ricezione chiamata viene impostata su 2.

  - La regola di ricezione chiamata viene impostata per consentire ai chiamanti di interrompere il messaggio di saluto.

<!-- end list -->

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

In questo esempio lo stato di disponibilità viene cambiato in Fuori sede per la regola di ricezione chiamata `MyCallAnsweringRule` nella cassetta postale di Tony Smith e viene impostata la priorità 2.

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith@contoso.com -ScheduleStatus 0x8


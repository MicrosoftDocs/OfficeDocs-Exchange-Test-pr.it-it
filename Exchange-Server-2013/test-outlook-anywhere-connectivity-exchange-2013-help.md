---
title: 'Verificare la connettività Outlook via Internet: Exchange 2013 Help'
TOCTitle: Verificare la connettività Outlook via Internet
ms:assetid: 0dc5b68f-2316-446a-84c9-5f1c50dc3776
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633453(v=EXCHG.150)
ms:contentKeyID: 50555539
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Verificare la connettività Outlook via Internet

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

È possibile verificare la connettività di Outlook Anywhere su client end-to-end tramite Shell o Analizzatore connettività remota di Exchange (ExRCA). Questo test include la verifica della connettività attraverso il servizio di individuazione automatica, la creazione di un profilo utente e l'accesso alla cassetta postale utente. Tutti i valori necessari vengono recuperati dal servizio di individuazione automatica.

Per informazioni sulle altre attività di gestione relative a Outlook Anywhere, vedere [Outlook via Internet](outlook-anywhere-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Outlook Anywhere" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Verifica della connettività di Outlook Anywhere tramite Shell

Per utilizzare Shell per verificare la connettività di Outlook Anywhere, utilizzare il cmdlet **Test-OutlookConnectivity**.

Eseguire il comando riportato di seguito.

    Test-OutlookConnectivity -ProbeIdentity 'OutlookMailboxDeepTestProbe' -MailboxId tony@contoso.com -Hostname contoso.com


> [!NOTE]
> Il valore del parametro <EM>OutlookMailboxDeepTestProbe</EM> consente di verificare la connettività dal server Cassette postali. Per verificare la connettività dal server Accesso client, utilizzare <EM>OutlookMailboxCTPProbe</EM> come valore del parametro <EM>ProbeIdentity</EM>.



## Verifica della connettività di Outlook Anywhere tramite Analizzatore connettività remota di Exchange

Exchange Remote Connectivity Analyzer (ExRCA) è uno strumento basato su web consente di testare la connettività con vari protocolli di Exchange. È possibile accedere il ExRCA [qui](https://go.microsoft.com/fwlink/p/?linkid=167905).

1.  Sul sito Web ExRCA, sotto **Prove di connettività di Microsoft Office Outlook**, selezionare **Outlook Anywhere** e quindi Avanti in fondo alla pagina.

2.  Immettere le informazioni richieste nella schermata successiva, inclusi l'indirizzo di posta elettronica, il nome di dominio e utente e la password.

3.  Scegliere se utilizzare il servizio di individuazione automatica per rilevare le impostazioni del server oppure specificarle manualmente.

4.  Accettare la dichiarazione di non responsabilità, immettere il codice di verifica e selezionare **Verifica**.

5.  Selezionare **Esegui prova**.

## Come verificare se l'operazione ha avuto esito positivo?

Dopo il completamento dei test, sulla pagina Web vengono visualizzati i risultati. In un elenco vengono indicati gli eventuali errori rilevati.


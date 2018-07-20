---
title: 'Importazione ed esportazione istruzioni, gli annunci, menu e messaggi di saluto personalizzati: Exchange 2013 Help'
TOCTitle: Importazione ed esportazione istruzioni, gli annunci, menu e messaggi di saluto personalizzati
ms:assetid: e82da5d5-625f-4d8b-8d31-ac45513aacfd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee681667(v=EXCHG.150)
ms:contentKeyID: 54652891
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importazione ed esportazione istruzioni, gli annunci, menu e messaggi di saluto personalizzati

 

_**Si applica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile importare ed esportare i file audio registrati da usare con dia plan di messaggistica unificata e operatori automatici. Ad esempio, è possibile esportare e salvare una copia di un file audio se si esegue l'aggiornamento da una versione precedente di Exchange. Oppure, potrebbe essere necessario importare una copia di un'istruzione audio registrata prima di configurare un dial plan o un operatore automatico.

I file audio sono vengono utilizzati per i seguenti scopi:

  - Nei dial plan di messaggistica unificata, vengono utilizzati per le formule di benvenuto personalizzate e per gli annunci informativi. Vengono riprodotti quando gli utenti di Outlook Voice Access chiamano un numero di Outlook Voice Access.

  - Negli operatori automatici di messaggistica unificata, i file audio vengono utilizzati per i messaggi di saluto personalizzati per gli orari di ufficio e non di ufficio, per gli annunci informativi, le le istruzioni di menu e per i menu di navigazione. Vengono riprodotti quando i chiamanti chiamano un operatore automatico di messaggistica unificata.

I seguenti file audio sono supportati per i messaggi di saluto, gli annunci, i menu e le istruzioni personalizzate:

  - File con estensione wma codificati con Windows Media Audio 9.2 - 96 kbps/44 kHz/stereo CBR di 1 sessione (Registratore di suoni Windows)

  - File Windows Media Audio Voice 9 - 8 kbps/8 kHz/Mono e file con estensione wav codificati con codec audio Linear PCM (16 bit/campione) a 8 kHz

Importare i file audio utilizzati dai dial plan e dagli operatori automatici di messaggistica unificata nella cassetta postale denominata {e0dc1c29-89c3-4034-b678-e6c29d823ed9} ed esportare i file audio da tale cassetta postale di sistema. I file audio possono essere importati ed esportati utilizzando i cmdlet **Import-UMPrompt** e **Export-UMPrompt**.

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" e "operatori automatici di messaggistica unificata? voci nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md) .

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di Shell per importare messaggi di saluto, annunci, menu e istruzioni personalizzate per i dial plan e gli operatori automatici di messaggistica unificata

Con questo esempio il file della formula di benvenuto welcomegreeting.wav viene importato dalla directory d:\\UMPrompts nel dial plan di messaggistica unificata `MyUMDialPlan`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

Con questo esempio il file della formula di benvenuto welcomegreeting.wav viene importato dalla directory d:\\UMPrompts nell'operatore automatico di messaggistica unificata `MyUMAutoAttendant`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

## Utilizzo di Shell per esportare messaggi di saluto, annunci, menu e istruzioni personalizzate dai dial plan e dagli operatori automatici di messaggistica unificata

Con questo esempio la formula di benvenuto per il dial plan di messaggistica unificata `MyUMDialPlan` viene esportata e salvata con il nome welcomegreeting.mp3.

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav�? -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

Con questo esempio la formula di benvenuto per l'orario di ufficio utilizzata per l'operatore automatico di messaggistica unificata `MYUMAutoAttendant` viene esportata e file salvata con il nome BusinessHoursWelcomeGreeting.mp3.

    $prompt = Export-UMPrompt -BusinessHoursWelcomeGreeting -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "d:\UMPrompts\BusinessHoursWelcomeGreeting.wav" -Value $prompt.AudioData -Encoding Byte


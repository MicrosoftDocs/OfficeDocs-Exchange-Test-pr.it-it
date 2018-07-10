---
title: 'Abilitare una richiesta di menu personalizzate orario di ufficio: Exchange 2013 Help'
TOCTitle: Abilitare una richiesta di menu personalizzate orario di ufficio
ms:assetid: 89053e84-3490-4dc6-ade3-9b6c5dbf4020
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232116(v=EXCHG.150)
ms:contentKeyID: 50555633
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare una richiesta di menu personalizzate orario di ufficio

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-19_

È possibile personalizzare le istruzioni vocali del menu utilizzate dall'operatore automatico di messaggistica unificata durante l'orario di ufficio. Una volta creato l'operatore automatico di messaggistica unificata, viene utilizzata un'istruzione vocale predefinita ("Benvenuti nella messaggistica unificata") che i chiamanti ascoltano quando viene riprodotto il messaggio di saluto in orario di ufficio. Anche se non è necessario sostituire o modificare le istruzioni vocali predefinite, è probabile che si desideri personalizzare i messaggi di saluto e le istruzioni vocali del menu utilizzate con gli operatori automatici di messaggistica unificata. Dopo aver creato un file audio con le istruzioni vocali del menu per l'orario di ufficio, è necessario abilitare le voci di spostamento nel menu dell'operatore automatico di messaggistica unificata per l'orario di ufficio.

Se si desidera includere solo il nome dell'organizzazione o dell'azienda nell'istruzione vocale predefinita, è possibile immettere il nome nella casella **Nome azienda** dell'operatore automatico di messaggistica unificata. Per ulteriori informazioni, vedere [Immettere il nome della società](enter-a-business-name-exchange-2013-help.md).


> [!IMPORTANT]
> È necessario configurare gli orari di ufficio nell'operatore automatico. Per ulteriori informazioni, vedere <A href="configure-business-hours-exchange-2013-help.md">Configurare le ore lavorative</A>.



Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Creazione di un file WAV o WMA da utilizzare per le istruzioni vocali del menu.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Abilitazione delle istruzioni vocali personalizzate del menu in orario di ufficio tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata** selezionare l'operatore automatico di messaggistica unificata per cui si desidera abilitare istruzioni vocali del menu personalizzate per l'orario di ufficio, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata**, \> **Spostamento nei menu**, in **Spostamento nei menu in orario di ufficio** fare clic su **Modifica**, quindi su **Sfoglia** per individuare il file delle istruzioni vocali personalizzate del menu per l'orario di ufficio.
    

    > [!IMPORTANT]
    > Il file da utilizzare per le istruzioni vocali del menu deve essere un file WAV o WMA.



4.  Dopo avere individuato il file, fare clic su **Apri**, quindi su **Salva**.

## Abilitazione delle istruzioni vocali personalizzate del menu in orario di ufficio tramite Shell

In questo esempio vengono abilitate le istruzioni vocali del menu principale in orario di ufficio e vengono utilizzate istruzioni personalizzate denominate `businesshoursprompts.wav` nell'operatore automatico di messaggistica unificata `MyUMAutoAttendant`.

    Command Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursMainMenuCustomPromptEnabled $true -BusinessHoursMainMenuCustomPromptFilename BusinessHoursPrompts.wav

In questo esempio viene configurato un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant` per cui gli orari di ufficio configurati sono 10:45 - 13:15 (domenica), 09:00 - 17:00 (lunedì) e 09:00 - 16:30 (sabato) e per cui sono configurate sia le festività sia i messaggi di saluto "`New Year`" per il 02.01.2013 e "`Building Closed for Construction`" dal 24 al 28.04.2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

In questo esempio viene configurato un operatore automatico di messaggistica unificata denominato `MyAutoAttendant` e vengono abilitati i menu di spostamento in orario di ufficio in modo che, quando i chiamanti premono 1, le chiamate vengano inoltrate a un altro operatore automatico di messaggistica unificata denominato `SalesAutoAttendant`. Quando premono 2, le chiamate vengono inoltrate al numero di interno 12345 di `Support`, mentre quando premono 3 vengono inviate a un altro operatore automatico che riproduce un file audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"


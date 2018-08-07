---
title: 'Abilita saluto in orario non lavorativo: Exchange 2013 Help'
TOCTitle: Abilitare un personalizzata non di ufficio messaggio di saluto
ms:assetid: d4743805-bab0-4735-a1e0-2cea4e088e8c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232183(v=EXCHG.150)
ms:contentKeyID: 50555699
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare un personalizzata non di ufficio messaggio di saluto

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-30_

È possibile abilitare una formula personalizzata di benvenuto Orario non di ufficio per un operatore automatico di messaggistica unificata. La formula personalizzata di benvenuto Orario non di ufficio è il primo messaggio che i chiamanti ascoltano quando un operatore automatico di messaggistica unificata risponde alla chiamata durante l'orario non di ufficio. È probabile che si desideri personalizzare il messaggio di saluto.

Messaggistica unificata include un'istruzione di sistema predefinita da utilizzare durante l'orario non di ufficio. Anche se l'istruzione di sistema predefinita non deve essere sostituita o modificata, è possibile fornire una formula di benvenuto personalizzata. Si può creare un messaggio di saluto personalizzato nel formato file WAV o WMA che può essere utilizzato quando i chiamanti effettuano una chiamata all'operatore automatico di messaggistica unificata durante l'orario non di ufficio. Ad esempio, il messaggio può contenere una formula che indica che gli uffici sono chiusi.

Se si desidera includere il nome dell'organizzazione o dell'azienda come parte della formula di benvenuto predefinita, inserire il nome nel campo **Ragione sociale** nell'operatore automatico di messaggistica unificata. Per ulteriori informazioni, vedere [Immettere il nome della società](enter-a-business-name-exchange-2013-help.md).

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Creare un file WAV o WMA da utilizzare per il saluto.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Abilitazione di una formula personalizzata di benvenuto Orario non di ufficio tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per cui si desidera abilitare la formula personalizzata di benvenuto Orario non di ufficio, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata**, \> **Messaggi di saluto**, sotto **Messaggio di saluto Orario non di ufficio**, fare clic su **Modifica**, quindi su **Sfoglia** per individuare il file del messaggio di saluto Orario non di ufficio personalizzato creato prima di avviare la procedura.
    

    > [!IMPORTANT]
    > Il formato del file utilizzato per il saluto deve essere WAV o WMA.



4.  Una volta individuato il file, fare clic su **Apri**, quindi su **Salva**.

## Abilitazione di una formula personalizzata di benvenuto Orario non di ufficio tramite Shell

Con questo esempio viene abilitato il messaggio di saluto per l'orario non di ufficio utilizzando una formula personalizzata di benvenuto denominata `GreetingFile.wav` per l'operatore automatico di messaggistica unificata `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AfterHoursWelcomeGreetingEnabled $true -AfterHoursWelcomeGreetingFilename GreetingFile.wav

In questo esempio viene configurato un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant` per cui gli orari di ufficio configurati sono 10:45 - 13:15 (domenica), 09:00 - 17:00 (lunedì) e 09:00 - 16:30 (sabato) e per cui sono configurate sia le festività sia i messaggi di saluto "`New Year`" per il 02.01.2013 e "`Building Closed for Construction`" dal 24 al 28.04.2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

Con questo esempio viene configurato un operatore automatico di messaggistica unificata denominato `MyAutoAttendant` e viene abilitata l'associazione dei tasti negli orari non di ufficio in modo che, quando i chiamanti premono 1, le chiamate vengano inoltrate a un altro operatore automatico di messaggistica unificata denominato `SalesAutoAttendant`. Quando premono 2, le chiamate vengono inoltrate al numero di interno 12345 di `Support`, mentre quando premono 3 vengono inviate a un altro operatore automatico che riproduce un file audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"


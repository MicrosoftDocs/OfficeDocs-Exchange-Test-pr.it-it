---
title: 'Abilitare una richiesta di menu personalizzate non di ufficio: Exchange 2013 Help'
TOCTitle: Abilitare una richiesta di menu personalizzate non di ufficio
ms:assetid: 094c50b2-072b-4929-aaf8-f7db5b19e9b6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb266919(v=EXCHG.150)
ms:contentKeyID: 50555534
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare una richiesta di menu personalizzate non di ufficio

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-03-22_

È possibile personalizzare le istruzioni di menu che verranno utilizzate da un operatore automatico di messaggistica unificata al di fuori dell'orario di ufficio. Dopo aver creato un operatore automatico di messaggistica unificata, viene utilizzato un prompt di sistema predefinito ("Benvenuti nella messaggistica unificata") come istruzioni di menu che i chiamanti ascoltano dopo la riproduzione dei saluti di benvenuto per l'orario non di ufficio. Anche se i prompt di sistema non devono essere sostituiti o modificati, è possibile personalizzare i messaggi di saluto e le istruzioni vocali del menu utilizzate con gli operatori automatici di messaggistica unificata. Dopo aver creato un file audio personalizzato con le istruzioni vocali del menu per l'orario non di ufficio, è necessario abilitare le opzioni del menu sull'operatore automatico di messaggistica unificata per l'orario non di ufficio.

Se si desidera includere solamente il nome dell'organizzazione o dell'azienda nel prompt di sistema predefinito, è possibile immettere il nome nella casella **Nome azienda** dell'operatore automatico di messaggistica unificata. Per ulteriori informazioni, vedere [Immettere il nome della società](enter-a-business-name-exchange-2013-help.md).


> [!IMPORTANT]
> È necessario configurare gli orari di ufficio nell'operatore automatico. Quando si configura l'orario di ufficio, l'orario non di ufficio viene impostato automaticamente. Per ulteriori informazioni, vedere <A href="configure-business-hours-exchange-2013-help.md">Configurare le ore lavorative</A>.



Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Informazioni necessarie prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Creare un file .wav o .wma da utilizzare per il prompt menu principale.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per abilitare istruzioni vocali del menu personalizzate per l'orario non di ufficio

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per cui si desidera abilitare le istruzioni vocali personalizzate del menu per l'orario non di ufficio, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata** \> **Spostamento nei menu**, in **postamento nei menu in orario non di ufficio**, scegliere **Modifica**, quindi **Sfoglia** per individuare il file delle istruzioni vocali personalizzate del menu per l'orario non di ufficio.
    

    > [!IMPORTANT]
    > Il file utilizzato per le istruzioni vocali del menu deve essere un file .wav o .wma.



4.  Una volta individuato il file, fare clic su **Apri**, quindi su **Salva**.

## Utilizzo di Shell per abilitare le istruzioni vocali personalizzate del menu per l'orario non di ufficio

In questo esempio viene abilitato un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant` per cui gli orari di ufficio configurati sono 10:45 - 13:15 (domenica), 09:00 - 17:00 (lunedì) e 09:00 - 16:30 (sabato) e per cui sono configurate sia le festività sia i messaggi di saluto, cioé "`New Year`" per il 01.01.13 e "`Building Closed for Construction`" dal 24 al 28.04.13.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

Con questo esempio viene configurato un operatore automatico di messaggistica unificata denominato `MyAutoAttendant` e vengono abilitati i menu di spostamento per l'orario non di ufficio in modo che, quando i chiamanti premono 1, le chiamate vengano inoltrate a un altro operatore automatico di messaggistica unificata denominato `SalesAutoAttendant`. Quando si preme 2, le chiamate vengono inoltrate al numero di interno 12345 per `Support`, mentre quando si preme 3 vengono inviate a un altro operatore automatico di messaggistica unificata che riproduce un file audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - 
    AfterHoursKeyMappingEnabled $true -
    AfterHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"


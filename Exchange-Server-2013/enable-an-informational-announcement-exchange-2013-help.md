---
title: 'Abilitare un annuncio informativo: Exchange 2013 Help'
TOCTitle: Abilitare un annuncio informativo
ms:assetid: 07f6c13e-3781-4127-9321-f0f85f054259
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb266918(v=EXCHG.150)
ms:contentKeyID: 50555533
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare un annuncio informativo

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-04-19_

È possibile abilitare un messaggio informativo per un operatore automatico di messaggistica unificata. Se abilitato, il messaggio informativo verrà riprodotto immediatamente dopo il messaggio di saluto per l'orario di ufficio o di inattività. Per impostazione predefinita, non è stato configurato alcun messaggio informativo. Per abilitarlo, è necessario creare un file .wav o .wma che verrà utilizzato come messaggio informativo e configurare l'operatore automatico per l'utilizzo del file audio.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Informazioni necessarie prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Creare un file .wav o .wma da utilizzare per il messaggio informativo.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare l'interfaccia di amministrazione di Exchange per abilitare un messaggio informativo

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per il quale si desidera abilitare il messaggio informativo, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata**, \> **Messaggi di saluto**, in **Messaggio informativo** fare clic su **Cambia**, quindi su **Sfoglia** per individuare il messaggio informativo creato prima di avviare questa procedura.
    

    > [!IMPORTANT]
    > Il file da utilizzare per il messaggio di saluto deve essere in formato .wav o .wma.



4.  Una volta individuato il file, fare clic su **Apri**, quindi su **Salva**.

## Abilitazione di un messaggio informativo tramite Shell

In questo esempio viene abilitato un messaggio informativo che utilizza il file `MyInfoAnnouncement.wav` su un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -InfoAnnouncementEnabled $true -InfoAnnouncementFilename MyInfoAnnouncement.wav


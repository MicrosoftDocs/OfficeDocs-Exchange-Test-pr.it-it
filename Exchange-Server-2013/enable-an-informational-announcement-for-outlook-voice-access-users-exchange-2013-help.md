---
title: 'Abilitare un annuncio informativo per gli utenti di Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Abilitare un annuncio informativo per gli utenti di Outlook Voice Access
ms:assetid: b69ed0e1-f978-498a-963e-42a047678db4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124344(v=EXCHG.150)
ms:contentKeyID: 50555674
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare un annuncio informativo per gli utenti di Outlook Voice Access

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

È possibile abilitare un messaggio informativo su un dial plan di messaggistica unificata. I messaggi informativi vengono utilizzati per messaggi generici che cambiano con maggior frequenza rispetto alla formula di benvenuto, oppure per messaggi richiesti dai criteri di conformità aziendali.

Per impostazione predefinita, i chiamanti, compresi gli utenti di Outlook Voice Access che chiamano il numero di Outlook Voice Access configurato, non ascoltano il messaggio informativo. Se si desidera che un messaggio informativo venga riprodotto, è necessario creare un file WAV o WMA da utilizzare con il messaggio informativo dopo aver creato un dial plan di messaggistica unificata, quindi abilitare il messaggio sul dial plan.

Quando è importante che venga ascoltato l'intero messaggio informativo, è possibile configurarlo in modo che non venga interrotto. In questo modo si evita che i chiamanti premano un tasto o pronuncino un comando per interrompere e arrestare il messaggio.

Per ulteriori informazioni sulle opzioni di menu disponibili per gli utenti di Outlook Voice Access, vedere la Guida di riferimento rapido per Outlook Voice Access, disponibile dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=272767).

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Abilitazione di un messaggio informativo tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  In **Outlook Voice Access**, sotto **Messaggio informativo**, fare clic su **Modifica**, quindi su **Sfoglia** per individuare il file del messaggio.
    

    > [!IMPORTANT]
    > Il formato del file utilizzato per il messaggio informativo deve essere WAV o WMA.



5.  Una volta individuato il file, fare clic su **Apri**, quindi su **Salva**.

## Abilitazione di un messaggio informativo tramite Shell

Con questo esempio viene abilitato un messaggio informativo che utilizza il file informational.wav su un dial plan di messaggistica unificata denominato `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -InfoAnnouncementEnabled $true-InfoAnnouncementFilename c:\UMGreetings\informational.wav


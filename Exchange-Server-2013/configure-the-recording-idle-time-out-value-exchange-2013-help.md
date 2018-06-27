---
title: 'Configurare il valore di timeout di inattività di registrazione: Exchange 2013 Help'
TOCTitle: Configurare il valore di timeout di inattività di registrazione
ms:assetid: a7fb9a09-fde9-447d-ad2c-95598405e99b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423550(v=EXCHG.150)
ms:contentKeyID: 50481388
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il valore di timeout di inattività di registrazione

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-11_

È possibile specificare il numero di secondi di silenzio che il sistema consente quando viene registrato un messaggio vocale prima che la chiamata viene terminata. Per la maggior parte delle organizzazioni, impostare questo valore per il valore predefinito pari a 5 secondi.

Questo valore può essere impostato tra 2 e 10. Se si imposta questo valore troppo basso può causare il sistema disconnettere i chiamanti prima di aver terminato l'uscita i messaggi vocali. Impostando questo valore troppo alto consente di lunga durata Disattiva nei messaggi vocali.

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare EAC per configurare il valore di timeout di inattività di registrazione

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  Nella finestra **Impostazioni** in **registrazione timeout di inattività (secondi)** immettere il numero di secondi.

5.  Fare clic su **Salva**.

## Utilizzo della Shell per configurare il valore di timeout di inattività di registrazione

In questo esempio imposta il valore di timeout di inattività di registrazione a 10 per un dial plan di messaggistica unificata denominato `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -RecordingIdleTimeout 10


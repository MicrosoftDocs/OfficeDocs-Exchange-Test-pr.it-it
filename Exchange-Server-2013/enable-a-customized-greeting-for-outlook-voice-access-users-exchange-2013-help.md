---
title: 'Consenti saluto person. per utenti Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Consentire a un messaggio di saluto personalizzato per gli utenti di Outlook Voice Access
ms:assetid: abd418ec-2c65-4720-859d-c11a2698dc06
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124125(v=EXCHG.150)
ms:contentKeyID: 50555660
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire a un messaggio di saluto personalizzato per gli utenti di Outlook Voice Access

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Per impostazione predefinita, ciascun dial plan di messaggistica unificata utilizza un file WAV standard per la formula di benvenuto riprodotta ai chiamanti, inclusi gli utenti di Outlook Voice Access che chiamano il numero di Outlook Voice Access configurato. È tuttavia possibile creare un file WAV o WMA per la formula di benvenuto, quindi abilitarlo nel dial plan di messaggistica unificata.

È ad esempio possibile che si desideri modificare questa formula di benvenuto predefinita con una specifica per la propria società, ad esempio "Benvenuti in Outlook Voice Access per Woodgrove Bank." A questo scopo, si registra il messaggio di benvenuto personalizzato e si salva come file WAV o WMA. Si configura quindi il dial plan per utilizzare la formula di benvenuto personalizzata.

Per ulteriori informazioni sulle opzioni di menu disponibili per gli utenti di Outlook Voice Access, vedere la Guida di riferimento rapido per Outlook Voice Access, disponibile dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=272767).

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Abilitazione di una formula di benvenuto personalizzata tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  In **Outlook Voice Access**, sotto **Formula di benvenuto**, fare clic su **Modifica**, quindi su **Sfoglia** per individuare il file della formula di benvenuto.
    

    > [!IMPORTANT]
    > Il formato del file utilizzato per la formula di benvenuto deve essere WAV o WMA.



5.  Una volta individuato il file, fare clic su **Apri**, quindi su **Salva**.

## Abilitazione di una formula di benvenuto personalizzata tramite Shell

Con questo esempio viene abilitata una formula di benvenuto che utilizza il file C:\\UMPrompts\\welcome.wav per un dial plan di messaggistica unificata denominato `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename c:\UMPrompts\welcome.wav


---
title: 'Modificare il codec audio: Exchange 2013 Help'
TOCTitle: Modificare il codec audio
ms:assetid: 139b2ccd-28c5-46c0-9050-777f4f59aade
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996342(v=EXCHG.150)
ms:contentKeyID: 50480029
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare il codec audio

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

La messaggistica unificata può utilizzare uno dei quattro codec per la creazione di messaggi vocali: MP3, Windows Media Audio (WMA), Group System Mobile (GSM) 06.10 e G.711 Pulse Code Modulation (PCM) Linear. Per impostazione predefinita, quando si crea un dial plan di messaggistica unificata, questo utilizza il codec audio MP3 per registrare i messaggi vocali. Il formato MP3 è un formato audio particolarmente diffuso utilizzato tra più sistemi operativi, client di posta elettronica e lettori MP3. Dopo aver creato il dial plan di messaggistica unificata, è possibile configurarlo per l'uso di uno degli altri formati codec audio (WMA, GSM 06.10 o G.711 PCM Linear). Per ascoltare un messaggio vocale, è necessario che sul telefono cellulare o sul computer sia installata un'applicazione audio compatibile.

Per altre attività relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per la modifica del codec audio su un dial plan di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  In **Impostazioni**, utilizzare l'elenco a discesa **Codec audio** per selezionare uno dei seguenti formati:
    
      - MP3
    
      - WMA
    
      - GSM
    
      - G711

5.  Fare clic su **Salva**.

## Modifica del codec audio su un dial plan di messaggistica unificata tramite Shell

In questo esempio, viene impostato il codec audio su un dial plan di messaggistica unificata denominato `MyUMDialPlan` su G.711.

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec G711

In questo esempio, viene impostato il codec audio su un dial plan di messaggistica unificata denominato `MyUMDialPlan` su WMA.

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec Wma


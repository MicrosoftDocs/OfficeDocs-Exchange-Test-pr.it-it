---
title: 'Configurare la directory di prelievo e la directory di riesecuzione: Exchange 2013 Help'
TOCTitle: Configurare la directory di prelievo e la directory di riesecuzione
ms:assetid: c9ca7358-9a08-4f57-89d0-910e4438df8a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124549(v=EXCHG.150)
ms:contentKeyID: 50481685
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la directory di prelievo e la directory di riesecuzione

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-08_

Le directory di prelievo e di riesecuzione vengono utilizzate dal servizio di trasporto sui server Cassette postali e Trasporto Edge per inserire i file dei messaggi direttamente nella pipeline di trasporto. I file dei messaggi di posta elettronica formattati correttamente e copiati nella directory di prelievo o riesecuzione vengono inviati per il recapito. La directory di prelievo viene utilizzata dagli amministratori per la verifica del flusso di posta o dalle applicazioni che devono creare e inviare i propri messaggi. La directory di riesecuzione riceve i messaggi da server gateway esterni non SMTP e reinoltra i messaggi esportati dalle code dei server Microsoft Exchange.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Servizio di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Il valore del parametro *PickupDirectoryMaxMessagesPerMinute* nel cmdlet **Set-TransportService** viene utilizzato dalle directory di prelievo e riesecuzione.

  - La modifica del percorso della directory di prelievo o riesecuzione non provoca la copia dei file dei messaggi esistenti dal vecchio percorso al nuovo. Il nuovo percorso della directory di prelievo o riesecuzione è attivo quasi immediatamente dopo la modifica della configurazione, ma i file dei messaggi esistenti rimangono nel percorso vecchio.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Configurazione della directory di prelievo tramite Shell

Per configurare la directory di prelievo, utilizzare la seguente sintassi.

    Set-TransportService <ServerIdentity> -PickupDirectoryPath <LocalFilePath> -PickupDirectoryMaxHeaderSize <Size> -PickupDirectoryMaxRecipientsPerMessage <Integer> -PickupDirectoryMaxMessagesPerMinute <Integer>

In questo esempio vengono eseguite le modifiche seguenti alla directory di prelievo sul server Cassette postali denominato Exchange01:

  - Il percorso della directory di prelievo è impostato su D:\\Pickup Directory.

  - La dimensione massima consentita per le intestazioni dei messaggi in un file è aumentata a 96 KB.

  - Il numero massimo di destinatari consentiti in un file di messaggio è aumentato a 250.

  - La velocità massima di elaborazione dei messaggi per le directory di prelievo e riesecuzione viene aumentata a 200 messaggi al minuto.

<!-- end list -->

    Set-TransportService Exchange01 -PickupDirectoryPath "D:\Pickup Directory" -PickupDirectoryMaxHeaderSize 96KB -PickupDirectoryMaxRecipientsPerMessage 250 -PickupDirectoryMaxMessagesPerMinute 200


> [!NOTE]
> <UL>
> <LI>
> <P>Impostando il valore del parametro <EM>PickupDirectoryPath</EM> su <CODE>$null</CODE>, la directory di prelievo viene disabilitata.</P>
> <LI>
> <P>La directory specificata dal parametro <EM>PickupDirectoryPath</EM> e dal parametro <EM>ReplayDirectoryPath</EM> non può essere la stessa.</P></LI></UL>



## Configurazione della directory di riesecuzione tramite Shell

Per configurare la directory di riesecuzione, utilizzare la seguente sintassi.

    Set-TransportService <ServerIdentity> -ReplayDirectoryPath "C:\Replay Directory" <LocalFilePath> -PickupDirectoryMaxMessagesPerMinute <Integer>

In questo esempio vengono eseguite le modifiche seguenti alla directory di riesecuzione sul server Cassette postali denominato Exchange01:

  - Il percorso della directory di riesecuzione è impostato su D:\\Replay Directory.

  - La velocità massima di elaborazione dei messaggi per le directory di prelievo e riesecuzione viene aumentata a 200 messaggi al minuto.

<!-- end list -->

    Set-TransportService Exchange01 -ReplayDirectoryPath "D:\Replay Directory" -PickupDirectoryMaxMessagesPerMinute 200


> [!NOTE]
> <UL>
> <LI>
> <P>Impostando il valore del parametro <EM>ReplayDirectoryPath</EM> su <CODE>$null</CODE>, la directory di riesecuzione viene disabilitata.</P>
> <LI>
> <P>La directory specificata dal parametro <EM>PickupDirectoryPath</EM> e dal parametro <EM>ReplayDirectoryPath</EM> non può essere la stessa.</P></LI></UL>



## Come verificare se l'operazione ha avuto esito positivo

Per verificate di aver configurato correttamente le directory di prelievo e riesecuzione, effettuare le operazioni seguenti:

1.  Eseguire il comando indicato di seguito:
    
        Get-TransportService <ServerIdentity> | Format-List Pickup*,Replay*

2.  Verificare che i valori visualizzati siano quelli configurati.


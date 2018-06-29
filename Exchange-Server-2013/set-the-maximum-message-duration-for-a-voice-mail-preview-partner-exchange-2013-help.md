---
title: 'Impostare la durata massima dei messaggi per un partner di anteprima messaggio vocale: Exchange 2013 Help'
TOCTitle: Impostare la durata massima dei messaggi per un partner di anteprima messaggio vocale
ms:assetid: 18f928ff-f4cc-4eed-a466-de13388780b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff630912(v=EXCHG.150)
ms:contentKeyID: 51407343
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare la durata massima dei messaggi per un partner di anteprima messaggio vocale

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-13_

È possibile impostare la durata massima dei messaggi per un partner per l'anteprima della posta vocale su un criterio cassetta postale di messaggistica unificata. Una volta impostata la durata massima dei messaggi, l'impostazione verrà applicata a tutti gli utenti abilitati alla messaggistica unificata associati a tale criterio cassetta postale.


> [!NOTE]
> Utilizzare Management Shell per impostare la durata massima dei messaggi per un partner per l'anteprima della posta vocale.



Per ulteriori informazioni sul programma partner Anteprima di posta vocale, vedere [Advisor Anteprima messaggio vocale](voice-mail-preview-advisor-exchange-2013-help.md).

Per le altre attività di gestione relative agli utenti di posta, vedere [Procedure di anteprima messaggio vocale](voice-mail-preview-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Impostazione della durata massima dei messaggi per un partner per l'anteprima della posta vocale tramite Shell

In questo esempio, la durata massima dei messaggi per un partner per l'anteprima della posta vocale viene impostata su 300 secondi (5 minuti) per il criterio cassetta postale di messaggistica unificata denominato *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300


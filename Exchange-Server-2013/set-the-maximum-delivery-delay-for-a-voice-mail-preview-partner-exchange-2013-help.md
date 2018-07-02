---
title: 'Impostare il ritardo massimo recapito di un partner di anteprima messaggio vocale: Exchange 2013 Help'
TOCTitle: Impostare il ritardo massimo recapito di un partner di anteprima messaggio vocale
ms:assetid: c9a07f6d-6f7f-4036-9a4a-d668d21e2c76
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff630928(v=EXCHG.150)
ms:contentKeyID: 51407412
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare il ritardo massimo recapito di un partner di anteprima messaggio vocale

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-13_

È possibile impostare il ritardo di recapito massimo per un partner di Anteprima casella vocale in un criterio cassetta postale di messaggistica unificata. Una volta impostato il ritardo di recapito massimo, l'impostazione verrà applicata a tutti gli utenti abilitati alla messaggistica unificata collegati al relativo criterio cassetta postale di messaggistica unificata.


> [!NOTE]
> Per impostare il ritardo di recapito massimo per un partner di Anteprima casella vocale, è necessario utilizzare Shell.



Per ulteriori informazioni sul programma partner Anteprima casella vocale, vedere [Advisor Anteprima messaggio vocale](voice-mail-preview-advisor-exchange-2013-help.md).

Per le altre attività di gestione relative all'anteprima casella vocale, vedere [Procedure di anteprima messaggio vocale](voice-mail-preview-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo di Shell per impostare il ritardo di recapito massimo per un partner di Anteprima casella vocale

In questo esempio il ritardo di recapito massimo è impostato su 600 secondi (10 minuti) in un criterio cassetta postale di messaggistica unificata denominato *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy - VoiceMailPreviewPartnerMaxDeliveryDelay 600


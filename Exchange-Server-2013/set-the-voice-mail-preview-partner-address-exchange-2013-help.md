---
title: 'Imposta indirizzo partner Anteprima messaggio vocale: Exchange 2013 Help'
TOCTitle: Impostare l'indirizzo di partner Anteprima messaggio vocale
ms:assetid: 57fbed1e-1b14-4939-95e6-ef7c072f32a9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff630917(v=EXCHG.150)
ms:contentKeyID: 51407367
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare l'indirizzo di partner Anteprima messaggio vocale

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-13_

È possibile impostare un indirizzo del partner per l'anteprima di casella vocale su un criterio cassetta postale di messaggistica unificata. Una volta configurate le impostazioni dell'indirizzo partner per l'anteprima della casella vocale su un criterio cassetta postale di messaggistica unificata, le impostazioni configurate vengono applicate a tutti gli utenti abilitati alla messaggistica unificata che risultano associati a quel criterio cassetta postale.


> [!NOTE]
> È necessario utilizzare Exchange Management Shell per configurare un indirizzo partner per l'anteprima della casella vocale.



Per ulteriori informazioni sul programma partner per l'anteprima della casella vocale, vedere [Advisor Anteprima messaggio vocale](voice-mail-preview-advisor-exchange-2013-help.md).

Per le altre attività di gestione relative all'anteprima della casella vocale, vedere [Procedure di anteprima messaggio vocale](voice-mail-preview-procedures-exchange-2013-help.md).

## Informazioni necessarie per iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Configurazione dell'indirizzo partner per l'anteprima della casella vocale su un criterio cassetta postale di messaggistica unificata tramite Shell

In questo esempio, l'indirizzo partner per l'anteprima della casella vocale viene impostato su exumvmp@fabrikam.com sul criterio cassetta postale di messaggistica unificata *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com


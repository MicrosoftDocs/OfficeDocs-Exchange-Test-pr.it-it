---
title: 'Configurare i servizi partner Anteprima messaggio vocale per gli utenti: Exchange 2013 Help'
TOCTitle: Configurare i servizi partner Anteprima messaggio vocale per gli utenti
ms:assetid: 7bb914ca-5502-4e64-bae5-555034138d8a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff630920(v=EXCHG.150)
ms:contentKeyID: 51407389
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare i servizi partner Anteprima messaggio vocale per gli utenti

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile configurare un partner per l'anteprima della casella vocale su un criterio cassetta postale di messaggistica unificata. Una volta configurate le impostazioni per il partner per l'anteprima della casella vocale, quali l'ID partner per l'anteprima della casella vocale e l'indirizzo partner per l'anteprima della casella vocale, su un criterio cassetta postale di messaggistica unificata, le impostazioni configurate verranno applicate a tutti gli utenti abilitati alla messaggistica unificata collegati a tale criterio cassetta postale.


> [!NOTE]
> È necessario utilizzare Shell per configurare un partner per l'anteprima della casella vocale.



Per le attività di gestione aggiuntive relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Come eseguire l'operazione?

## Passaggio 1: Registrarsi con un servizio di partner

Per l'elenco dei partner certificati e istruzioni dettagliate su come effettuare l'iscrizione, vedere [Advisor Anteprima messaggio vocale](voice-mail-preview-advisor-exchange-2013-help.md) oppure visitare il sito Web [Microsoft individuare](https://go.microsoft.com/fwlink/p/?linkid=281966) . Dopo aver effettuato l'accesso, è necessario immettere il partner Anteprima messaggio vocale è un ID partner e l'indirizzo SMTP da utilizzare per inoltrare i messaggi vocali.

Nel passo 2, si applicheranno l'ID partner e l'indirizzo SMTP acquisiti nel passo 1 ai criteri cassetta postale di messaggistica unificata richiesti.

## Passaggio 2: Impostare l'ID e l'indirizzo partner per l'anteprima della casella vocale

In questo esempio, viene impostato l'indirizzo partner per l'anteprima della casella vocale su exumvmp@fabrikam.com e l'ID partner per l'anteprima della casella vocale su CON123-2010 su un criterio cassetta postale di messaggistica unificata denominato *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com
    -VoiceMailPreviewPartnerAssignedID CON123-2010

## Passaggio 3: Configurare le impostazioni avanzate del partner per l'anteprima della casella vocale

Se il partner richiede impostazioni personalizzate, è possibile che si desideri impostare due parametri aggiuntivi per un partner per l'anteprima della casella vocale, come indicato di seguito:

  - *VoiceMailPreviewPartnerMaxMessageDuration*

  - *VoiceMailPreviewPartnerMaxDeliveryDelay*

In questo esempio, viene impostata la durata massima del messaggio su 300 secondi (5 minuti) e il ritardo massimo di recapito su 600 secondi (10 minuti) su un criterio cassetta postale di messaggistica unificata denominato *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300 -VoiceMailPreviewPartnerMaxDeliveryDelay 600

## Passaggio 4: Assegnare un utente abilitato alla messaggistica unificata al criterio cassetta postale di messaggistica unificata per un partner per l'anteprima della casella vocale

Se si desidera configurare il servizio partner per l'anteprima della casella vocale per alcuni (ma non tutti) utenti abilitati alla messaggistica unificata in un dial plan di messaggistica unificata, è necessario creare un nuovo criterio cassetta postale di messaggistica unificata e configurare le impostazioni per il partner. Una volta terminato. è possibile applicare il nuovo criterio agli utenti abilitati alla messaggistica unificata selezionati. Per ulteriori informazioni su come assegnare un utente abilitato alla messaggistica unificata a un criterio cassetta postale di messaggistica unificata, vedere i seguenti argomenti:

  - [Assegnare un criterio cassetta postale di messaggistica unificata](assign-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/it-it/library/bb124893\(v=exchg.150\))

Per ulteriori informazioni sul programma partner Anteprima di posta vocale, vedere [Advisor Anteprima messaggio vocale](voice-mail-preview-advisor-exchange-2013-help.md).


---
title: 'Configurare un dial plan per gli utenti con nomi simili: Exchange 2013 Help'
TOCTitle: Configurare un dial plan per gli utenti con nomi simili
ms:assetid: 14783f45-95f5-49de-8215-0a3aef7dc034
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb266943(v=EXCHG.150)
ms:contentKeyID: 51407339
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare un dial plan per gli utenti con nomi simili

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

È possibile configurare un dial plan di messaggistica unificata per specificare le informazioni fornite per i chiamanti quando gli utenti possiedono nomi uguali o simili. La messaggistica unificata utilizza questa impostazione per distinguere tra utente che hanno nomi uguali o simili e fornire tale informazioni ai chiamanti. Quando a un chiamante o a un utente di Outlook Voice Access viene richiesto di immettere le lettere per trovare un determinato utente, a volte più nomi corrispondono all'input del chiamante. È possibile utilizzare una delle opzioni disponibili per fornire al chiamante ulteriori informazioni che consentano di individuare l'utente cercato.

È possibile configurare tale impostazione sia nei dial plan che negli operatori automatici di messaggistica unifica. Quando viene creato un operatore automatico di messaggistica unificata, quest'ultimo eredita questa impostazione dal dial plan ad esso associato. Per impostazione predefinita, tale impostazione non viene configurata per i dial plan, per questo motivo nessuna ulteriore informazione verrà data ai chiamanti per aiutarli a individuare l'utente corretto.


> [!NOTE]
> Affinché le informazioni che verranno incluse per gli utenti con nomi simili funzionino correttamente, è necessario fornire informazioni su titolo, reparto e posizione dei destinatari nell'organizzazione Microsoft Exchange.



Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare l'interfaccia di amministrazione di Exchange per configurare un dial plan di messaggistica unificata per gli utenti con nomi simili

1.  Nell'interfaccia di amministrazione di Exchange, passare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata da modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura** \> **Transferimento e ricerca** e in **Informazioni da includere sugli utenti con lo stesso nome**, selezionare una delle opzioni seguenti:
    
      - **Titolo**   Il dial plan include il titolo di ogni utente quando trova due o più utente con nomi simili.
    
      - **Reparto**   Il dial plan include il reparto di ogni utente quando trova due o più utente con nomi simili.
    
      - **Posizione**   Il dial plan include la posizione di ogni utente quando trova due o più utente con nomi simili.
    
      - **Nessuna**   Il dial plan non include alcuna informazione aggiuntiva quando gli utenti possiedono nomi simili. Sebbene questa sia l'impostazione predefinita, si consiglia di includere una delle opzioni disponibili per i chiamanti. In caso contrario, i chiamanti non potranno distinguere due o più utente con nomi simili.
    
      - **Prompt per l'alias**   Il dial plan richiede al chiamante l'alias dell'utente. Un alias è la parte dell'indirizzo di posta elettronica o SMTP dell'utente che si trova prima del simbolo "at" o chiocciola (@).

3.  Fare clic su **Salva**.

## Utilizzare Shell per configurare un dial plan di messaggistica unificata per gli utenti con nomi simili

In questo esempio vengono impostate le informazioni da includere per gli utenti con nomi simili sulla richiesta dell'alias dell'utente per il dial plan di messaggistica unificata denominato `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod PromptForAlias

In questo esempio vengono impostate le informazioni da includere per gli utenti con nomi simili nel reparto in un dial plan di messaggistica unificata denominato `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Department

In questo esempio vengono impostate le informazioni da includere per gli utenti con nomi simili per una posizione in un dial plan di messaggistica unificata denominato `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Location


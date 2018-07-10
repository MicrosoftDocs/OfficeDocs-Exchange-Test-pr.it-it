---
title: 'Configurare il gruppo di utenti che possono contattare gli utenti di Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurare il gruppo di utenti che possono contattare gli utenti di Outlook Voice Access
ms:assetid: a8dc0f9e-dc86-4128-af63-d4e550aed5bb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423551(v=EXCHG.150)
ms:contentKeyID: 50481393
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il gruppo di utenti che possono contattare gli utenti di Outlook Voice Access

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-09_

È possibile specificare quali utenti ricevono le chiamate o i messaggi della segreteria telefonica trasferiti dagli utenti di Outlook Voice Access. L'opzione **Solo in questo dial plan** è selezionata per impostazione predefinita. È possibile cambiare questa impostazione per consentire agli utenti di Outlook Voice Access di trasferire le chiamate o inviare messaggi vocali agli utenti nell'intera organizzazione, a un operatore automatico di messaggistica unificata esistente o a un numero di interno specifico.

Per altre attività relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Utilizzare EAC per configurare il gruppo di utenti che gli utenti di Outlook Voice Access possono contattare

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  In **Trasferisci e cerca**, nella sezione **Consenti a chiamanti di cercare gli utenti in base al nome o all'alias**, selezionare una delle seguenti opzioni:
    
      - **Solo in questo dial plan**   Utilizzare questa opzione per consentire agli utenti di Outlook Voice Access che chiamano un numero di Outlook Voice Access di individuare e contattare gli utenti all'interno dello stesso dial plan.
    
      - **Nell'intera organizzazione**   Utilizzare questa opzione per consentire agli utenti di Outlook Voice Access che chiamano un numero di Outlook Voice Access di individuare e contattare chiunque nell'intera organizzazione. Sono inclusi tutti gli utenti che sono abilitati all'utilizzo della cassetta postale.
    
      - **Solo questo operatore automatico**   Utilizzare questa opzione per consentire agli utenti di Outlook Voice Access che chiamano un numero di Outlook Voice Access di connettersi a un operatore automatico specifico. È necessario creare l'operatore automatico prima di specificarlo qui. In questo modo gli utenti di Outlook Voice Access possono essere trasferiti a un altro operatore automatico. L'operatore automatico scelto può essere abilitato o non abilitato alla sintesi vocale.
    
      - **Solo questo interno**   Utilizzare questa opzione per consentire agli utenti di Outlook Voice Access di collegarsi al numero di interno specificato. È possibile utilizzare solo cifre numeriche per l'interno. Il numero di cifre fornito in questo campo deve corrispondere al numero di cifre del numero di interno configurato nel dial plan di messaggistica unificata.

5.  Fare clic su **Salva**.

## Utilizzare Shell per configurare il gruppo di utenti che gli utenti di Outlook Voice Access possono contattare

In questo esempio viene impostato il gruppo di utenti che gli utenti di Outlook Voice Access possono contattare per un dial plan di messaggistica unificata denominato `MyUMDialPlan` nell'intera organizzazione.

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope 'GlobalAddressList' -UMAutoAttendant $null -AllowDialPlanSubscribers $false -AllowExtensions $false

In questo esempio viene impostato il gruppo di utenti che gli utenti di Outlook Voice Access possono contattare per un dial plan di messaggistica unificata denominato `MyUMDialPlan` in `DialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope DialPlan -AllowDialPlanSubscribers $false -AllowExtensions $false


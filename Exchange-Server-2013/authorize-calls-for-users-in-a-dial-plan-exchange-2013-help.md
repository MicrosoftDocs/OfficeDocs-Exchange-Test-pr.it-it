---
title: 'Autorizzare chiamate per gli utenti in un dial plan: Exchange 2013 Help'
TOCTitle: Autorizzare chiamate per gli utenti in un dial plan
ms:assetid: 7c7fd0c4-4001-408e-b352-c49bac9f78cc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb691175(v=EXCHG.150)
ms:contentKeyID: 51407378
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzare chiamate per gli utenti in un dial plan

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

È possibile abilitare le autorizzazioni di composizione su un dial plan di messaggistica unificata. Le autorizzazioni di composizione su un dial plan sono utilizzate per impedire a utenti non autenticati di Outlook Voice Access di effettuare chiamate a numeri di telefono nazionali o internazionali oppure *chiamate esterne*. Le chiamate esterne vengono effettuate quando Messaggistica unificata esegue una chiamata esterna per un utente dopo aver chiamato un numero di telefono di Outlook Voice Access configurato su un dial plan di messaggistica unificata. Quando si configura un'impostazione su un dial plan di messaggistica unificata, tale impostazione si applica a tutti gli utenti non autenticati che chiamano un numero di Outlook Voice Access.

Per le attività di gestione aggiuntive correlate alle chiamate esterne, vedere [Che consente agli utenti di effettuare chiamate procedure](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire la procedura, confermare che le regole di composizione di numeri nazionali e internazionali siano state create su un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creare regole di composizione per gli utenti](create-dialing-rules-for-users-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Abilitazione delle autorizzazioni di composizione su un dial plan di messaggistica unificata per i gruppi di regole di composizione nazionali tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Nuovo dial plan di messaggistica unificata** fare clic su **Configura**.

3.  Nella pagina **Dial plan di messaggistica unificata** \> **Autorizzazione di composizione**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") in **Gruppi di regole di composizione nazionali consentiti**.

4.  Nella pagina **Seleziona gruppi di regole di composizione per consentire**, selezionare il gruppo di regole di composizione, fare clic su **OK**, quindi su **Salva**.

## Abilitazione delle autorizzazioni di composizione su un dial plan di messaggistica unificata per i gruppi di regole di composizione internazionali tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Nuovo dial plan di messaggistica unificata** fare clic su **Configura**.

3.  Nella pagina **Dial plan di messaggistica unificata** \> **Autorizzazione di composizione**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") in **Gruppi di regole di composizione internazionali consentiti**.

4.  Nella pagina **Seleziona gruppi di regole di composizione per consentire**, selezionare il gruppo di regole di composizione, fare clic su **OK**, quindi su **Salva**.

## Abilitazione delle autorizzazioni di composizione internazionali e nazionali su un dial plan di messaggistica unificata tramite Shell

In questo esempio vengono abilitate le autorizzazioni di composizione InCountry/RegionGroup1, InCountry/RegionGroup2, InternationalGroup1 e InternationalGroup2 su un dial plan di messaggistica unificata denominato `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2


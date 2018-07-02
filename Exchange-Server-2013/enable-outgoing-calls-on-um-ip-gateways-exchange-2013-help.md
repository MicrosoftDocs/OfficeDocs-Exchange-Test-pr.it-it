---
title: 'Abilitare le chiamate in uscita sui gateway IP di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Abilitare le chiamate in uscita sui gateway IP di messaggistica unificata
ms:assetid: c3ad8e53-d37e-499e-b1f1-defb0ba1bd12
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673562(v=EXCHG.150)
ms:contentKeyID: 50481631
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare le chiamate in uscita sui gateway IP di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-13_

Se disabilitate, le chiamate in uscita possono essere abilitate per un gateway IP di messaggistica unificata. Quando si seleziona l'opzione **Consenti chiamate in uscita tramite questo gateway IP di messaggistica unificata** nelle proprietà per il gateway IP di messaggistica unificata, si configura il gateway IP di messaggistica unificata per accettare e inviare le chiamate in uscita verso gateway VoIP (Voice over IP), PBX (Private Branch eXchange) abilitati per SIP (Session Initiation Protocol), PBX IP o SBC (Session Border Controller). Anche se l'impostazione **Consenti chiamate in uscita tramite questo gateway IP di messaggistica unificata** controlla la capacità del gateway IP di messaggistica unificata di avviare le chiamate in uscita per gli utenti, non influisce sui trasferimenti di chiamata o sulle chiamate in arrivo da gateway VoIP, PBX abilitati per SIP, PBX IP o SBC.

Con l'espressione *effettuazione di una chiamata esterna* si intende una situazione in cui un utente in un dial plan di messaggistica unificata avvia una chiamata verso un utente abilitato alla messaggistica unificata in un altro dial plan o verso un numero di telefono esterno.

Per consentire le chiamate esterne agli utenti abilitati alla messaggistica unificata, è necessario:

  - Verificare che le chiamate esterne siano consentite sul gateway IP di messaggistica unificata.

  - Creare gruppi di regole di composizione tramite la creazione di voci di regole di composizione nel dial plan di messaggistica unificata associato al gateway IP di messaggistica unificata.

  - Aggiungere i gruppi di regole di composizione corretti all'elenco delle restrizioni di composizione in **Autorizzazione di composizione** nel dial plan di messaggistica unificata, nell'operatore automatico o nei criteri cassetta postale di messaggistica unificata.

Per altre attività di gestione relative ai gateway IP di messaggistica unificata, vedere [Procedure di gateway IP di messaggistica unificata](um-ip-gateway-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gateway IP di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È indispensabile confermare la creazione di un gateway IP di messaggistica unificata prima di eseguire queste procedure. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Abilitazione delle chiamate in uscita per gateway IP di messaggistica unificata tramite EAC

1.  Nell'Interfaccia di amministrazione di Exchange, andare a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, selezionare il gateway IP di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Gateway IP di messaggistica unificata**, deselezionare la casella di controllo accanto a **Consenti chiamate in uscita tramite questo gateway IP di messaggistica unificata**.

3.  Fare clic su **Salva**.

## Abilitazione delle chiamate in uscita per gateway IP di messaggistica unificata tramite Shell

Con questo esempio vengono abilitate le chiamate in uscita su un gateway IP di messaggistica unificata denominato `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $true


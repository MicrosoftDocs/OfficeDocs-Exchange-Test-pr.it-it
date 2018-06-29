---
title: 'Disabilitare le chiamate in uscita sui gateway IP di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Disabilitare le chiamate in uscita sui gateway IP di messaggistica unificata
ms:assetid: a3777cc6-37e4-4359-ada3-a962ac0ef0c3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232153(v=EXCHG.150)
ms:contentKeyID: 50481311
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare le chiamate in uscita sui gateway IP di messaggistica unificata

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-13_

È possibile abilitare o disabilitare le chiamate in uscita per un gateway IP di messaggistica unificata. Se si deseleziona la casella di controllo **Consenti chiamate in uscita tramite questo gateway IP di messaggistica unificata** nelle proprietà del gateway IP di messaggistica unificata, il gateway viene configurato per non accettare e inviare chiamate in uscita verso un gateway Voice over IP (VoIP), un IP-PBX o un Session Border Controller (SBC). Anche se l'impostazione **Consenti chiamate in uscita tramite questo gateway IP di messaggistica unificata** controlla la capacità del gateway IP di messaggistica unificata di avviare le chiamate in uscita per gli utenti, non influisce sui trasferimenti di chiamata o sulle chiamate in arrivo da un gateway VoIP, un IP-PBX o un SBC.

Per altre attività di gestione relative ai gateway IP di messaggistica unificata, vedere [Procedure di gateway IP di messaggistica unificata](um-ip-gateway-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gateway IP di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È indispensabile confermare la creazione di un gateway IP di messaggistica unificata prima di eseguire queste procedure. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Utilizzare EAC per disabilitare le chiamate in uscita per un gateway IP di messaggistica unificata

1.  Nell'Interfaccia di amministrazione di Exchange, andare a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, selezionare il gateway IP di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Gateway IP di messaggistica unificata**, deselezionare la casella di controllo accanto a **Consenti chiamate in uscita tramite questo gateway IP di messaggistica unificata**.

3.  Fare clic su **Salva**.

## Utilizzare Shell per disabilitare le chiamate in uscita per un gateway IP di messaggistica unificata

In questo esempio vengono disabilitate le chiamate in uscita su un gateway IP di messaggistica unificata denominato `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $false


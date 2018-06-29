---
title: 'Disabilitare un gateway IP di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Disabilitare un gateway IP di messaggistica unificata
ms:assetid: fe3a8797-1230-49cb-a839-ccec238266b6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125257(v=EXCHG.150)
ms:contentKeyID: 50482133
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare un gateway IP di messaggistica unificata

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-13_

Per impostazione predefinita, quando viene creato un gateway IP di messaggistica unificata, lo stato di tale gateway è impostato su abilitato. Una volta creato il gateway IP di messaggistica unificata, è possibile disabilitarlo impostandone lo stato su disabilitato. Una volta disabilitato il gateway IP di messaggistica unificata, il gateway VoIP (Voice over IP), PBX (IP Private Branch eXchange) o SBC (Session Border Controller) configurati per l'utilizzo non saranno più in grado di elaborare le chiamate di messaggistica unificata in arrivo.

Per altre attività di gestione relative ai gateway IP di messaggistica unificata, vedere [Procedure di gateway IP di messaggistica unificata](um-ip-gateway-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gateway IP di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È indispensabile confermare la creazione e l'abilitazione di un gateway IP di messaggistica unificata prima di eseguire queste procedure. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md) e [Abilitare un gateway IP di messaggistica unificata](enable-a-um-ip-gateway-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Disabilitazione di un gateway IP di messaggistica unificata tramite l'interfaccia di amministrazione di Exchange

1.  Nell'Interfaccia di amministrazione di Exchange, andare a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, selezionare il gateway IP di messaggistica unificata che si desidera modificare, quindi fare clic su **Freccia Giù**![Icona Freccia in giù](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icona Freccia in giù").

2.  Nella pagina **Avviso** fare clic su **Sì**.

## Disabilitazione di un gateway IP di messaggistica unificata tramite Shell

In questo esempio viene disabilitato un gateway IP di messaggistica unificata denominato `MyUMIPGateway` e viene interrotta l'accettazione delle chiamate in arrivo dal gateway VoIP, IP PBX o SPC.

    Disable-UMIPGateway -Identity MyUMIPGateway

In questo esempio viene disabilitato un gateway IP di messaggistica unificata denominato `MyUMIPGateway` e vengono disconnesse immediatamente tutte le chiamate correnti.

    Disable-UMIPGateway -Identity MyUMIPGateway -Immediate $true


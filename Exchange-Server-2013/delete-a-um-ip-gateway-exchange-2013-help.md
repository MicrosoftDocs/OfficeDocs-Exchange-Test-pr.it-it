---
title: 'Eliminare un gateway IP di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Eliminare un gateway IP di messaggistica unificata
ms:assetid: 569d3741-67dd-4597-8d28-010011be0c12
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998214(v=EXCHG.150)
ms:contentKeyID: 50480636
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eliminare un gateway IP di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

Quando viene eliminato un gateway IP di messaggistica unificata, i server di Exchange non sono più in grado di accettare le chiamate in ingresso dai gateway VoIP, PBX abilitato per SIP, IP PBX o session border controller (SBC) associati al gateway IP di messaggistica unificata.


> [!IMPORTANT]
> È consigliabile eliminare un gateway IP di messaggistica unificata solo dopo aver compresso le implicazioni della disabilitazione delle comunicazioni tramite gateway VoIP, PBX IP o SBC.



Per altre attività relative ai gateway IP di messaggistica unificata, vedere [Procedure di gateway IP di messaggistica unificata](um-ip-gateway-procedures-exchange-2013-help.md).

## Informazioni necessarie per iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gateway IP di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È indispensabile confermare la creazione di un gateway IP di messaggistica unificata prima di eseguire queste procedure. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per l'eliminazione di un gateway IP di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, selezionare il gateway IP di messaggistica unificata che si intende eliminare, quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

2.  Nella pagina **Avviso** fare clic su **Sì**.

## Eliminazione di un gateway IP di messaggistica unificata tramite Shell

In questo esempio, il gateway IP di messaggistica unificata `MyUMIPGateway` viene eliminato.

    Remove-UMIPGateway -Identity MyUMIPGateway


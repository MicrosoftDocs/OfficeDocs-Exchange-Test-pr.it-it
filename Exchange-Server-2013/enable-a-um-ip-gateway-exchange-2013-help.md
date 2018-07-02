---
title: 'Abilitare un gateway IP di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Abilitare un gateway IP di messaggistica unificata
ms:assetid: 2706ae06-c45d-41b7-abbe-378a9fca104a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996857(v=EXCHG.150)
ms:contentKeyID: 50480278
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare un gateway IP di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-05_

Per impostazione predefinita, quando un gateway IP di messaggistica unificata viene creato, il suo stato è abilitato. Tuttavia, potrebbe essere necessario disabilitare il gateway IP di messaggistica unificata per metterlo offline e non permettergli di ricevere chiamate in ingresso e in uscita. Dopo aver creato un gateway IP di messaggistica unificata, è possibile controllarne il funzionamento impostando la variabile di stato su abilitato o disabilitato.

Per altre attività di gestione relative ai gateway IP di messaggistica unificata, vedere [Procedure di gateway IP di messaggistica unificata](um-ip-gateway-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gateway IP di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, è necessario verificare che il gateway IP di messaggistica unificata sia stato creato e disabilitato. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Utilizzo dell'interfaccia di amministrazione di Exchange per l'abilitazione di un gateway IP di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, selezionare il gateway IP di messaggistica unificata che si desidera abilitare, quindi fare clic sulla **freccia su**![Icona Freccia in su](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "Icona Freccia in su").

2.  Nella pagina **Avviso** fare clic su **Sì**.

## Abilitazione di un gateway IP di messaggistica unificata tramite Shell

In questo esempio viene abilitato un gateway IP di messaggistica unificata denominato `MyUMIPGateway`.

    Enable-UMIPGateway -Identity MyUMIPGateway


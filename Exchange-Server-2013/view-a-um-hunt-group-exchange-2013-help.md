---
title: 'Visualizza gruppo risposta messaggistica unificata: Exchange 2013 Help'
TOCTitle: Visualizzare un gruppo di risposta di messaggistica unificata
ms:assetid: f038f7b4-4de9-4373-bd58-09d49e37a3ed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125167(v=EXCHG.150)
ms:contentKeyID: 50555694
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzare un gruppo di risposta di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-05_

Quando vengono visualizzate le proprietà di un gruppo di risposta di messaggistica unificata, è possibile visualizzare le proprietà associate a uno o a tutti i gruppi di risposta di messaggistica unificata associati a un singolo gateway IP di messaggistica unificata. Se non viene specificato alcun parametro, verranno restituiti tutti i gruppi di risposta di messaggistica unificata. Non è possibile utilizzare EAC per visualizzare le proprietà dei gruppi di risposta di messaggistica unificata, è necessario utilizzare Shell.

Una volta creato un gruppo di risposta di messaggistica unificata, non è possibile modificare le impostazioni configurate. Per modificare un'impostazione di configurazione come l'identificatore pilota in un gruppo di risposta di messaggistica unificata, è necessario eliminare il gruppo di risposta di messaggistica unificata esistente e crearne uno nuovo con le impostazioni corrette.

Per altre attività relative ai gruppi di risposta di messaggistica unificata, vedere [Procedure gruppo di risposta di messaggistica unificata](um-hunt-group-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di risposta di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un gateway di messaggistica unificata. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un gruppo di risposta di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un gruppo di risposta di messaggistica unificata](create-a-um-hunt-group-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Visualizzazione delle proprietà di un gruppo di risposta di messaggistica unificata tramite Shell

In questo esempio vengono visualizzati tutti i gruppi di risposta di messaggistica unificata nella foresta Active Directory.

    Get-UMHuntGroup

In questo esempio vengono visualizzati i dettagli del gruppo di risposta di messaggistica unificata denominato `MyUMHuntGroup` in un elenco formattato.

    Get-UMHuntGroup -identity MyUMIPGateway\MyUMHuntGroup | Format-List


> [!NOTE]
> Quando si utilizza il cmdlet <STRONG>Get-UMHuntGroup</STRONG>, non è possibile immettere unicamente il nome del gruppo di risposta di messaggistica unificata. ma è necessario includere anche il nome del gateway IP di messaggistica unificata associato a tale gruppo.



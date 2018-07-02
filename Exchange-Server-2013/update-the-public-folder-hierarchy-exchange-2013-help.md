---
title: 'Aggiornamento della gerarchia di cartelle pubbliche: Exchange 2013 Help'
TOCTitle: Aggiornamento della gerarchia di cartelle pubbliche
ms:assetid: a7b2fb51-0207-4d7d-938d-466ae110bb90
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945055(v=EXCHG.150)
ms:contentKeyID: 52057318
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiornamento della gerarchia di cartelle pubbliche

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2014-04-03_

Per avviare manualmente la sincronizzazione delle cartelle e l'assistente cassette postali, è sufficiente aggiornare la la gerarchia delle cartelle pubbliche. Entrambi vengono avviati almeno una volta ogni 24 ore per ciascuna cassetta postale delle cartelle pubbliche nell'organizzazione. La sincronizzazione della gerarchia viene avviata ogni 15 minuti se esistono utenti che hanno effettuato l'accesso a una cassetta postale secondaria tramite Microsoft Outlook o un client di Servizi Web di Microsoft Exchange.

Per ulteriori attività di gestione relative alle cartelle pubbliche in Exchange Online, vedere [Procedure per le cartelle pubbliche in Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/jj966272\(v=exchg.150\)).

Per ulteriori attività di gestione relative alle cartelle pubbliche in Exchange Server 2013, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cartelle pubbliche" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Non è possibile eseguire questa procedura nell'interfaccia di amministrazione di Exchange, è necessario utilizzare Shell.

  - Quando si esegue questo comando con il parametro *InvokeSynchronizer*, si consiglia di utilizzare il parametro *SuppressStatus*. Se non si utilizza questo parametro nel comando, nell'output verranno visualizzati messaggi di stato ogni 3 secondi per un minuto. Finché non è trascorso un minuto, non è possibile utilizzare quella istanza di Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Aggiornamento della gerarchia di cartelle pubbliche

In questo esempio viene aggiornata la gerarchia si cartelle pubbliche nella casella postale delle cartelle pubbliche PF\_marketing e viene eliminato l'output del comando.

    Update-PublicFolderMailbox -Identity PF_marketing -InvokeSynchronizer -SuppressStatus

In questo esempio vengono aggiornate tutte le cassette postali delle cartelle pubbliche e viene eliminato l'output del comando.

    Get-Mailbox -PublicFolder | Update-PublicFolderMailbox InvokeSynchronizer -SuppressStatus


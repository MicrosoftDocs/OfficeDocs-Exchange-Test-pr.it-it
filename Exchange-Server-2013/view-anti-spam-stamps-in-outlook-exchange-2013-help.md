---
title: 'Visualizzazione di indicatori di protezione da posta indesiderate in Outlook: Exchange 2013 Help'
TOCTitle: Visualizzazione di indicatori di protezione da posta indesiderate in Outlook
ms:assetid: cddb5dbf-ad1e-471c-9fc8-28ddcf7ec1d0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124595(v=EXCHG.150)
ms:contentKeyID: 50481727
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzazione di indicatori di protezione da posta indesiderate in Outlook

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

È possibile utilizzare Microsoft Outlook per visualizzare gli indicatori di protezione da posta indesiderata applicati da Microsoft Exchange a un messaggio di posta elettronica. Gli indicatori di protezione da posta indesiderata permettono di effettuare una diagnosi dei problemi relativi alla posta indesiderata applicando i metadati diagnostici o gli indicatori, come le informazioni specifiche sul mittente, i risultati della convalida puzzle e di filtro contenuto, ai messaggi quando passano attraverso gli agenti di protezione da posta indesiderata che filtrano i messaggi in ingresso da Internet.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Accesso alle cassette postali" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Visualizzazione degli gli indicatori di protezione da posta indesiderata tramite Outlook 2010 oppure Outlook 2013

1.  In Outlook 2010 o Outlook 2013, su un computer client, nella visualizzazione **Posta**, fare doppio clic su un messaggio per aprirlo.

2.  Nella sezione **Tag** della barra multifunzione fare clic sull'icona **Opzioni** per visualizzare la finestra di dialogo **Proprietà** del messaggio.

3.  Nella finestra di dialogo **Proprietà**, nella sezione **Intestazioni Internet** utilizzare la barra di scorrimento per visualizzare gli indicatori di protezione da posta indesiderata, come mostrato nell'esempio seguente.
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

## Visualizzazione degli indicatori filtro di posta indesiderata tramite Outlook 2007

1.  In Outlook 2007, su un computer client, nella schermata **Posta**, fare doppio clic su un messaggio per aprirlo.

2.  Nella scheda **Messaggio**, fare clic su **Opzioni messaggio** nel gruppo **Opzioni**.

3.  Nella finestra di dialogo **Opzioni messaggio**, nella sezione **Intestazioni Internet**, usare la barra di scorrimento per visualizzare i contrassegni filtro posta indesiderata come mostrato nell'esempio seguente.
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures


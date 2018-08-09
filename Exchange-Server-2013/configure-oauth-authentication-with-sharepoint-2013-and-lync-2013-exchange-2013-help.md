---
title: 'Conf. autentic. OAuth con SharePoint 2013 e Lync 2013: Exchange 2013 Help'
TOCTitle: Configurazione dell'autenticazione OAuth con SharePoint 2013 e Lync 2013
ms:assetid: ca3c78a3-80cc-4df2-859f-0106bbd57a07
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ649094(v=EXCHG.150)
ms:contentKeyID: 50481688
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione dell'autenticazione OAuth con SharePoint 2013 e Lync 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-03-03_

Exchange Server 2013 consente ad altre applicazioni di utilizzare OAuth per l'autenticazione in Exchange. Le applicazioni devono essere configurate come applicazioni partner in Exchange 2013.

In Exchange 2013 la configurazione di OAuth con applicazioni partner quali SharePoint 2013 e Lync Server 2013 è supportata solo utilizzando lo script `Configure-EnterpriseApplication.ps1`. Se si automatizza l'attività, lo script semplifica la configurazione dell'autenticazione con le applicazioni partner riducendo gli errori. Lo script consente di eseguire le attività riportate di seguito:

1.  Configura un'applicazione partner aziendale che emette automaticamente i token OAuth per l'autenticazione corretta in Exchange.

2.  Assegna i ruoli RBAC (controllo di accesso basato sui ruoli) all'applicazione partner per l'autorizzazione alla chiamata di API specifiche di Servizi Web Exchange.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - L'applicazione partner deve pubblicare un documento con metadati di autorizzazione per Exchange 2013 per stabilire un trust diretto nell'applicazione e accettare le richieste di autenticazione.

  - Gli esempi presenti in questo argomento utilizzano la posizione predefinita della directory `\Scripts`: `C:\Program Files\Microsoft\Exchange Server\V15\Scripts`.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Applicazioni partner: configurazione" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurazione dell'autenticazione OAuth con un'applicazione partner

In questa procedura viene utilizzato lo script `Configure-EntepririseApplication.ps1` per configurare l'autenticazione OAuth con le applicazioni partner. L'accesso alle risorse dipende dalle autorizzazioni assegnate all'applicazione partner e/o dall'utente rappresentato utilizzando RBAC.

Dopo la configurazione dell'autenticazione OAuth da Exchange, l'applicazione partner può utilizzare le risorse Exchange 2013. Se anche Exchange 2013 necessita dell'accesso alle risorse offerte dall'applicazione partner, è necessario configurare anche l'autenticazione OAuth nell'applicazione partner.

In questo esempio viene configurata l'autenticazione OAuth per SharePoint 2013.

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://sharepoint.contoso.com/_layouts/15/metadata/json/1 -ApplicationType SharePoint

In questo esempio viene configurata l'autenticazione OAuth per Lync Server 2013.

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://lync.contoso.com/metadata/json/1 -ApplicationType Lync

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver configurato correttamente un'applicazione partner aziendale per l'autenticazione in Exchange 2013, eseguire il cmdlet [Get-PartnerApplication](https://technet.microsoft.com/it-it/library/jj218721\(v=exchg.150\)) in Shell per recuperare la configurazione. È inoltre possibile eseguire il cmdlet [Test-OAuthConnectivity](https://technet.microsoft.com/it-it/library/jj218623\(v=exchg.150\)) per verificare la connettività OAuth con un'applicazione partner per un utente.

## Ulteriori informazioni

  - Nelle distribuzioni ibride, è possibile utilizzare l'autenticazione OAuth tra l'organizzazione locale di Exchange 2013 e quella di Exchange Online. Per ulteriori informazioni, vedere [Utilizzo dell'autenticazione OAuth per supportare eDiscovery in un'implementazione ibrida di Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md).

  - Nelle distribuzioni locali, è possibile configurare l'autenticazione da server a server tra Exchange 2013 e SharePoint 2013. In questo modo modo, gli amministratori e i responsabili della conformità possono utilizzare il centro eDiscovery in SharePoint 2013 per effettuare ricerche delle cassette postali di Exchange 2013. Per ulteriori informazioni, vedere [Configurare Exchange per SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).


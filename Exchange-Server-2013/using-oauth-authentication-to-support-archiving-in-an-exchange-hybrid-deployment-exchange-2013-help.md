---
title: 'Autent. OAuth supporta archiv. in distr. ibride Exchange: Exchange 2013 Help'
TOCTitle: Utilizzo dell'autenticazione OAuth per supportare l'archiviazione nelle distribuzioni ibride di Exchange
ms:assetid: deb882b1-1ae2-40f3-a71c-423fafe3d66a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn689104(v=EXCHG.150)
ms:contentKeyID: 62247345
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzo dell'autenticazione OAuth per supportare l'archiviazione nelle distribuzioni ibride di Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Se ti trovi in una distribuzione ibrida di Exchange 2013 e usi Exchange Online Archiving (EOA) per Exchange Server, devi configurare l'autenticazione OAuth nell'organizzazione locale e in Exchange Online, dopo aver eseguito l'aggiornamento cumulativo 5 di Exchange 2013 (CU5). EOA ti consente di disporre di un archivio basato sul cloud per gli utenti con cassette postali locali. In questa situazione, l'assistente alla gestione record di messaggistica (MRM) del server relativo alla tua cassetta postale locale applica i criteri di archiviazione e sposta automaticamente i messaggi da una cassetta postale dell'utente all'archivio sul cloud. In Exchange 2013 CU5, viene utilizzata l'autenticazione OAuth.

Per istruzioni dettagliati sul come configurare l'autenticazione OAuth, vedi [Configurazione dell'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## Che cosa si intende per autenticazione OAuth?

L'autenticazione OAuth consiste in un protocollo di autenticazione tra server che consente alle applicazione di autenticarsi a vicenda. Grazie all'autenticazione OAuth, le credenziali e le password dell'utente non vengono trasferite da un computer all'altro. Invece, l'autenticazione e l'autorizzazione sono processi basati sullo scambio di token di sicurezza, i quali garantiscono l'accesso a un set specifico di risorse per un determinato periodo di tempo.

L'autenticazione OAuth in genere tra tre parti: un server singolo autorizzazioni e le due aree che necessitano di comunicare tra loro. I token di sicurezza vengono inviati dal server di autorizzazione (noto anche come un security token server) per le due aree che necessitano di comunicare; Questi token verificare che le comunicazioni provenienti da un'area di autenticazione devono essere considerato attendibile da altri area di autenticazione. Quando si utilizza l'autenticazione OAuth tra un'organizzazione di Exchange locale ed Exchange Online, la funzione di server di autorizzazione è fornita dall' Servizi di controllo per l'accesso ad Azure Active Directory (ACS) nella propria organizzazione Office 365. Ad esempio durante una ricerca eDiscovery cross-premise, Servizio di controllo di accesso Azure Active Directory genera token che consentono di verificare che un amministratore o responsabile della conformità da Exchange locali dell'organizzazione è in grado di accedere alle cassette postali nell'organizzazione Exchange Online e viceversa.

## Configurazione dell'autenticazione OAuth per supportare l'archiviazione

Come detto in precedenza, vedi [Configurazione dell'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md) per istruzioni su come configurare l'autenticazione OAuth per supportare l'archiviazione in una distribuzione ibrida di Exchange.

Se OAuth non è configurato per la tua distribuzione ibrida di Exchange, non puoi usare i criteri di archiviazione per spostare automaticamente gli elementi dalla cassetta principale di un utente della tua organizzazione locale nell'archivio basato sul cloud in Exchange Online.

## Ulteriori informazioni

  - Inoltre, devi configurare l'autenticazione OAuth per eseguire ricerche eDiscovery cross-premise delle cassette postali locali e basate sul cloud di una singola ricerca eDiscovery. Vedi [Utilizzo dell'autenticazione OAuth per supportare eDiscovery in un'implementazione ibrida di Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md).

  - Puoi anche configurare l'autenticazione OAuth per consentire altre applicazioni, ad esempio SharePoint 2013 e Lync Server 2013, per l'autenticazione a Exchange 2013. Per ulteriori informazioni, vedi [Configurazione dell'autenticazione OAuth con SharePoint 2013 e Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

  - Puoi configurare l'autenticazione tra server specifici in Exchange 2013 e SharePoint 2013 in modo che gli amministratori e i responsabili della conformità possano usare il centro eDiscovery in SharePoint 2013 per cercare le cassette postali di Exchange 2013. Per ulteriori informazioni, vedi [Configurare Exchange per SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

  - È possibile configurare una distribuzione ibrida di Exchange utilizzando la procedura guidata Configurazione ibrida in Exchange 2013. Per elenco di controllo configurazione distribuzione ibrida dettagliato e personalizzato, vedere [Exchange Server Deployment Assistant](https://go.microsoft.com/fwlink/p/?linkid=277105).


---
title: 'Configurare Exchange per SharePoint eDiscovery Center: Exchange 2013 Help'
TOCTitle: Configurare Exchange per SharePoint eDiscovery Center
ms:assetid: 795c1a3b-295c-4ee5-ade9-52cf3fda3f19
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ218665(v=EXCHG.150)
ms:contentKeyID: 50480928
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare Exchange per SharePoint eDiscovery Center

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Microsoft Exchange Server 2013 include funzionalità che interagiscono con Microsoft SharePoint Server 2013 e Microsoft Lync Server 2013, chiamate anche *applicazioni partner*. Affinché queste applicazioni partner possano reciprocamente accedere alle rispettive risorse, è necessario configurare l'autenticazione da server a server.

In questo argomento viene illustrato come configurare l'autenticazione da server a server tra Exchange 2013 e SharePoint 2013 in modo che gli utenti possono utilizzare il centro eDiscovery in SharePoint 2013 per cercare contenuto delle cassette postali Exchange Server 2013. Per poter utilizzare questa funzionalità, è necessario eseguire ulteriori passaggi in SharePoint 2013. Per ulteriori informazioni, vedere [Configure eDiscovery in SharePoint 2013](https://go.microsoft.com/fwlink/?linkid=257727).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 30 minuti.

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - È possibile installare Exchange 2013 e SharePoint 2013 in domini o foreste differenti. Una relazione di trust di Windows tra foreste Exchange e SharePoint non è necessaria perché in tale circostanza Exchange e SharePoint si basano sul protocollo OAuth 2.0 per confermare l'attendibilità reciproca.

  - Il sito SharePoint 2013 deve essere configurato per l'utilizzo di SSL (Secure Sockets Layer).

  - [Exchange Web Services Managed API](https://go.microsoft.com/fwlink/?linkid=257726) deve essere installato in ogni server che esegue SharePoint 2013. Reimpostare Internet Information Server (IIS) dopo l'installazione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: Configurare l'autenticazione da server a server per Exchange 2013 su un server con SharePoint Server 2013

Utilizzare il seguente comando per creare Exchange 2013 come emittente di token di sicurezza attendibile in SharePoint 2013.
```powershell
    New-SPTrustedSecurityTokenIssuer -Name Exchange -MetadataEndPoint https://<Exchange Server Name or FQDN>/autodiscover/metadata/json/1
```
## Passaggio 2: Configurare l'autenticazione da server a server per SharePoint 2013 su un server con Exchange 2013

Eseguire questo passo su un server Exchange 2013. Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Applicazioni partner: configurazione" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

Utilizzare il seguente comando per configurare l'applicazione partner di SharePoint.
```powershell
    cd c:\'Program Files'\Microsoft\'Exchange Server'\V15\Scripts
    .\Configure-EnterprisePartnerApplication.ps1 -AuthMetadataUrl <path to SharePoint AuthMetadataUrl> -ApplicationType SharePoint
```
## Passaggio 3: Aggiungere gli utenti autorizzati al gruppo di ruoli Gestione individuazione

Aggiungere gli utenti che devono eseguire una ricerca eDiscovery utilizzando SharePoint 2013 al gruppo di ruoli Gestione individuazione in Exchange 2013. Per ulteriori informazioni, vedere [Assegnare le autorizzazioni di eDiscovery di Exchange](https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions).


> [!WARNING]
> L'aggiunta degli utenti al gruppo di ruoli Gestione individuazione consente loro di utilizzare la funzionalità eDiscovery in locale per cercare in tutte le cassette postali di Exchange 2013 e accedere a contenuti potenzialmente riservati nelle cassette postali degli utenti. Per impostazione predefinita, questa autorizzazione non viene assegnata ad alcun utente, inclusi i membri del gruppo di ruoli Gestione organizzazione. Rivolgersi all'ufficio legale o all'ufficio del personale dell'organizzazione prima di assegnare questa autorizzazione agli utenti.



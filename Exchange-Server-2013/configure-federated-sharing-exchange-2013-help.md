---
title: 'Configurare la condivisione federata: Exchange 2013 Help'
TOCTitle: Configurare la condivisione federata
ms:assetid: b25ae450-def3-4797-a5fc-6e9bcee71a5d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657483(v=EXCHG.150)
ms:contentKeyID: 50481466
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la condivisione federata

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

La condivisione federata in Exchange Server 2013 consente agli utenti di condividere le informazioni con i destinatari delle organizzazioni federate esterne. È compresa la condivisione delle informazioni sulla disponibilità, nota anche come disponibilità di calendario per scopi di pianificazione oppure, in base alla natura della relazione di organizzazione, la condivisione di informazioni di calendario più dettagliate. Per ulteriori informazioni sulla condivisione federata, vedere [Condivisione](sharing-exchange-2013-help.md).


> [!IMPORTANT]
> Questa funzionalità di Exchange Server 2013 non è completamente compatibile con Office 365 utilizzato da 21Vianet in Cina e potrebbe essere soggetta a limitazioni. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/?linkid=313640">Informazioni su Office 365 utilizzato da 21Vianet</A>.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 1 ora.

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: Creare e configurare una relazione di trust federativa

Una relazione di trust federativa stabilisce una relazione di trust tra le organizzazioni Exchange 2013 e il sistema di autenticazione Azure Active Directory e costituisce un requisito per la condivisione federata.

Per istruzioni dettagliate, vedere [Configurazione di una relazione di trust federativa](configure-a-federation-trust-exchange-2013-help.md).

## Passaggio 2: Creare una relazione di organizzazione

Una relazione dell'organizzazione consente agli utenti dell'organizzazione di Exchange condividere le informazioni sulla disponibilità del calendario come parte della condivisione federata con altre organizzazioni Exchange federate. Condivisione federata può essere configurata tra due organizzazioni federate Exchange 2013 o tra un'organizzazione federata Exchange 2013 e alle organizzazioni federate Exchange 2010.

Per istruzioni dettagliate, vedere [Creare una relazione dell'organizzazione](create-an-organization-relationship-exchange-2013-help.md).

## Passaggio 3: Creare un criterio di condivisione

I criteri di condivisione consentono la condivisione stabilita dall'utente e tra utenti delle informazioni di calendario con tipi diversi di utenti esterni. Supportano la condivisione delle informazioni di contatto e di calendario con le organizzazioni federate esterne, con le organizzazioni non federate esterne e con singoli utenti che dispongono dell'accesso a Internet. Se non è necessario configurare una condivisione tra utenti o delle informazioni di contatto (solo condivisione a livello di organizzazione), il criterio di condivisione non deve essere configurato.

Per istruzioni dettagliate, vedere [Creare un criterio di condivisione](create-a-sharing-policy-exchange-2013-help.md).

## Passaggio 4: Configurare un record DNS pubblico di individuazione automatica

È necessario aggiungere un record di risorse alias CNAME (nome canonico) a DNS con connessione pubblica. Il nuovo record CNAME deve puntare a un server Accesso client Exchange 2013 connesso a Internet su cui viene eseguito il servizio di individuazione automatica.

Per istruzioni dettagliate sulla modalità di aggiunta di record CNAME, vedere il servizio host dei record DNS pubblici. Si tratta in genere di un servizio basato su Internet che può ospitare anche il sito Web del dominio.


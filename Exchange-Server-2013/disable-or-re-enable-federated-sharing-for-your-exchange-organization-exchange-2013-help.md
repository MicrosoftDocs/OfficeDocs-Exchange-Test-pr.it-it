---
title: "Disabilitare o riabilitare la condivisione federata per l'organizzazione di Exchange: Exchange 2013 Help"
TOCTitle: Disabilitare o riabilitare la condivisione federata per l'organizzazione di Exchange
ms:assetid: d36490d8-0268-47b9-a6d4-e56427f1b02e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657497(v=EXCHG.150)
ms:contentKeyID: 50481733
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare o riabilitare la condivisione federata per l'organizzazione di Exchange

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-02-17_

In alcuni casi potrebbe essere necessario disabilitare temporaneamente la condivisione federata per l'organizzazione. Anziché eliminare la relazione di trust federativa esistente o eliminare le relazioni dell'organizzazione e i criteri di condivisione che potrebbero essere necessari in futuro, è sufficiente disabilitare l'identificatore organizzazione (OrgID) per la relazione di trust federativa.


> [!WARNING]
> Per le distribuzioni ibride con Office 365, la disabilitazione della relazione di trust federativa per i server locali comporterà anche la disabilitazione di funzionalità ibride quali le informazioni sulla disponibilità del calendario condiviso, suggerimenti messaggio e verifica messaggi. Tuttavia, Secure Mail Transport non verrà disabilitato nella distribuzione ibrida se la relazione di trust federativa per l'organizzazione on-premises è disabilitata.



Per ulteriori informazioni sulle relazioni di trust federative, vedere [Federazione](federation-exchange-2013-help.md). Per ulteriori informazioni sulla condivisione federata, vedere [Condivisione](sharing-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alla condivisione federata, vedere [Procedure di federazione](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Questa funzionalità di Exchange Server 2013 non è completamente compatibile con Office 365 utilizzato da 21Vianet in Cina e potrebbe essere soggetta a limitazioni. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/?linkid=313640">Informazioni su Office 365 utilizzato da 21Vianet</A>.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Autorizzazioni *Federation and certificates* nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Le relazioni dell'organizzazione esistenti e i criteri di condivisione per le altre organizzazioni di Exchange federate non verranno modificate e non saranno attive. I criteri di condivisione configurati per fornire ai destinatari Internet l'accesso alle informazioni sul calendario non saranno interessati.

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per abilitare o disabilitare l'OrgID per una relazione di trust federativa. È necessario utilizzare la shell.

## Disabilitazione o nuova abilitazione della condivisione federata tramite Shell

In questo esempio vengono disabilitati l'OrgID, la federazione e la condivisione federata per l'organizzazione di Exchange.

    Set-FederatedOrganizationIdentifier -Enabled $false

In questo esempio viene abilitato l'OrgID e abilitate nuovamente la federazione e la condivisione federata per l'organizzazione di Exchange.

    Set-FederatedOrganizationIdentifier -Enabled $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/it-it/library/dd351037\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Il corretto completamento del cmdlet **Set-OrganizationIdentifier** sarà il primo segnale del fatto che OrgID è stato disabilitato o abilitato.

Per un ulteriore verifica, eseguire il comando della shell riportato di seguito e verificare il valore restituito per il parametro *Enabled*

    Get-FederatedOrganizationIdentifier


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



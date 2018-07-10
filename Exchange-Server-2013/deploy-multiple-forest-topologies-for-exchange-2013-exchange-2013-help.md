---
title: 'Distribuire più topologie a foresta di Exchange Server 2013: Exchange 2013 Help'
TOCTitle: Distribuire più topologie a foresta di Exchange Server 2013
ms:assetid: d51f2b7d-9045-40cf-8b9f-43787a6fff6d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124734(v=EXCHG.150)
ms:contentKeyID: 51407417
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Distribuire più topologie a foresta di Exchange Server 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questo argomento vengono fornite informazioni di carattere generale sulla distribuzione di Exchange Server 2013 in topologie a più foreste. Sono disponibili informazioni sui seguenti argomenti:

  - **Topologie a più foreste supportate**   Exchange 2013 supporta due tipi di topologie a più foreste: tra foreste e foresta di risorse.

  - **Sincronizzazione GAL**   In un ambiente tra foreste, è necessario assicurarsi che l'elenco indirizzi globale (GAL) di una determinata foresta contenga i destinatari di posta elettronica di altre foreste.

  - **Spostamento di cassette postali tra foreste**    I cmdlet **New-MoveRequest** e **New-MigrationBatch** in Exchange Management Shell consentono di spostare le cassette postali da una foresta all'altra.

  - **Informazioni sull'amministrazione di più foreste**   Informazioni sul modello di autorizzazioni per la configurazione e la gestione delle autorizzazioni tra foreste.

## Topologie a più foreste supportate

Exchange 2013 supporta i seguenti tipi di topologie a più foreste:

  - **Tra foreste** Una topologia tra foreste è una topologia con più foreste di Exchange. Di seguito viene fornita una panoramica degli elementi necessari per distribuire Exchange 2013 in una topologia con una foresta multipla:
    
    1.  È necessario installare prima Exchange 2013 in ogni foresta. Per ulteriori informazioni, vedere [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md).
    
    2.  È quindi necessario sincronizzare i destinatari in ciascuna delle foreste, in modo che l'elenco indirizzi globale (GAL) di ogni foresta contenga utenti provenienti da tutte le foreste sincronizzate. Per ulteriori dettagli, vedere la sezione "Sincronizzazione di un elenco indirizzi globale".
    
    3.  Infine è necessario configurare il servizio Disponibilità in modo che gli utenti di una foresta possano visualizzare i dati relativi alla disponibilità destinati agli utenti di un'altra foresta. Per ulteriori informazioni, vedere [Configurare il servizio disponibilità per topologie con più foreste](configure-the-availability-service-for-cross-forest-topologies-exchange-2013-help.md).
    
    Per ulteriori informazioni sulla distribuzione di Exchange 2013 in una topologia tra foreste, vedere [Distribuzione di Exchange 2013 in una topologia a più foreste](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md).

  - **Foresta di risorse**   Una topologia foresta di risorse è una topologia con una foresta di Exchange e una o più foreste di account utente. Di seguito viene fornita una panoramica degli elementi necessari per distribuire Exchange 2013 in una topologia con foresta di risorse:
    
    1.  È necessario disporre di una foresta in cui sia stato installato Exchange. Nella foresta di Exchange è necessario avere disabilitato gli account utente che dispongono di cassette postali di Exchange.
    
    2.  È necessario disporre di almeno una foresta contenente gli account utente. In questa foresta *non* deve essere installato Exchange.
    
    3.  È necessario quindi associare gli account utente disabilitati nella foresta di Exchange agli account utente nella foresta degli account.
    
    Per ulteriori informazioni sulla distribuzione di Exchange 2013 in una topologia con foresta di risorse, vedere [Distribuzione di Exchange 2013 in una topologia a foresta risorsa Exchange](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md).

## Sincronizzazione di un elenco indirizzi globale

Per impostazione predefinita, un elenco indirizzi globale include i destinatari di posta elettronica di una singola foresta. In un ambiente tra foreste, si consiglia di utilizzare Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) per assicurarsi che l'elenco indirizzi globale (GAL) di una determinata foresta contenga i destinatari di posta elettronica di altre foreste. ILM 2007 FP1 consente di creare utenti di posta elettronica che rappresentano destinatari di altre foreste, in modo che gli utenti siano in grado di visualizzarli nell'elenco indirizzi globale e utilizzarli per inviare messaggi. Ad esempio, gli utenti della foresta A vengono visualizzati come utenti di posta elettronica nella foresta B e viceversa. Gli utenti della foresta di destinazione possono inoltre selezionare l'utente di posta elettronica che rappresenta un destinatario in un'altra foresta e inviargli un messaggio.

Per abilitare la funzionalità di sincronizzazione degli elenchi indirizzi globali, è necessario creare agenti di gestione per l'importazione di utenti, contatti e gruppi abilitati all'utilizzo della posta da specifici servizi di Active Directory in una metadirectory centralizzata in cui gli oggetti abilitati all'utilizzo della posta sono rappresentati come utenti di posta elettronica, mentre i gruppi vengono rappresentati come contatti senza appartenenze associate. Gli agenti di gestione esportano quindi gli utenti di posta elettronica in un'unità organizzativa della foresta di destinazione specificata.

Per ulteriori informazioni su Forefront Identity Manager (FIM), vedere [Forefront Identity Manager 2010](https://go.microsoft.com/fwlink/p/?linkid=279864).

## Spostamento di cassette postali tra foreste

In una topologia con più foreste, si potrebbe voler spostare le cassette di posta da una foresta all'altra. Per eseguire tale operazione, è necessario utilizzare il cmdlet **New-MoveRequest** o il cmdlet **New-MigrationBatch** in Exchange Management Shell. Per ulteriori informazioni sullo spostamento delle cassette postali tra foreste, vedere i seguenti argomenti:

  - [Preparare le cassette postali per le richieste di spostamento tra foreste](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Prepara le cassette postali per gli spostamenti tra foreste utilizzando lo script Prepare MoveRequest.ps1 in Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

  - [Preparare le cassette postali per gli spostamenti tra foreste con codice di esempio](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

## Informazioni sull'amministrazione di più foreste

Per gestire ambienti a più foreste in Exchange 2013 viene utilizzata la nuova funzionalità per le autorizzazioni.

Exchange 2013 utilizza un modello di autorizzazioni di controllo di accesso basato sui ruoli (RBAC, Role Based Access Control). I gruppi di ruoli di gestione di cui gli amministratori sono membri e i criteri di assegnazione dei ruoli di gestione a cui gli utenti finali sono associati determinano le operazioni che ogni amministratore e ogni utente finale può eseguire. Per comprendere le autorizzazioni a più foreste, è necessario avere una certa familiarità con il controllo di accesso basato sui ruoli. Per ulteriori informazioni sul controllo di accesso basato sui ruoli, sui gruppi di ruoli e sui criteri di assegnazione dei ruoli, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

Per configurare e gestire le autorizzazioni tra foreste, è possibile utilizzare il modello di autorizzazioni RBAC. Per ulteriori informazioni sulle autorizzazioni in ambienti a più foreste, vedere i seguenti argomenti:

  - [Informazioni sulle autorizzazioni di più foreste](understanding-multiple-forest-permissions-exchange-2013-help.md)

  - [Gestire i gruppi di ruoli collegato](manage-linked-role-groups-exchange-2013-help.md)

  - [Creare gruppi di ruoli collegato il mirroring di gruppi di ruoli incorporati](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)


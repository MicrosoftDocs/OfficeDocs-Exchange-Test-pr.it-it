---
title: "Modifiche in AD con l'installazione di Exchange 2013: Exchange 2013 Help"
TOCTitle: Modifiche in Active Directory con l'installazione di Exchange 2013
ms:assetid: 07386078-6103-49a2-8698-2d41db9cec95
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn750898(v=EXCHG.150)
ms:contentKeyID: 62371319
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifiche in Active Directory con l'installazione di Exchange 2013

 

_**Si applica a:** Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-05-26_

Quando si installa Exchange 2013, vengono apportate modifiche ai domini e alla foresta di Active Directory. Exchange esegue tali modifiche in modo da poter archiviare le informazioni sui server e sulle cassette postali di Exchange e su altri oggetti correlati a Exchange nell'organizzazione. Le modifiche vengono effettuate quando si esegue l'Installazione guidata di Exchange 2013 o quando si eseguono i comandi *PrepareSchema*, *PrepareAD* e *PrepareDomains* (per l'utilizzo di questi comandi, vedere [Preparazione di Active Directory e dei domini](prepare-active-directory-and-domains-exchange-2013-help.md)) durante l'installazione da riga di comando di Exchange 2013. Questo argomento descrive le modifiche apportate da Exchange a Active Directory e illustra cosa fa Exchange a ogni passaggio della preparazione di Active Directory.

I passaggi da completare per preparare Active Directory per Exchange sono tre:

  - Extend the Active Directory schema

  - Prepare Active Directory containers, objects, and other items

  - Prepare Active Directory domains

Una volta terminati, la foresta Active Directory è pronta per Exchange 2013. Per saperne di più sull'installazione di Exchange 2013, consultare [Installazione di Exchange 2013 utilizzando l'installazione guidata](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

## Estendere lo schema di Active Directory

L'estensione dello schema di Active Directory consente di aggiungere classi, attributi e altri elementi. Tali modifiche sono necessarie perché Exchange possa creare contenitori e oggetti per archiviare informazioni sull'organizzazione Exchange. Poiché Exchange apporta numerose modifiche allo schema Active Directory, un argomento è dedicato a questo passaggio. Per visualizzare tutte le modifiche dello schema, vedere [Modifiche allo schema di Active Directory in Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

Questo passaggio viene eseguito automaticamente quando si esegue l'Installazione guidata di Exchange 2013 sul primo server Exchange 2013 della foresta Active Directory. Viene effettuato, inoltre, quando si esegue l'installazione da riga di comando di Exchange 2013 con il comando *PrepareSchema* (o *PrepareAD*) sul primo server Exchange 2013 della foresta. Per saperne di più sull'estensione dello schema, vedere [Extend the Active Directory schema](prepare-active-directory-and-domains-exchange-2013-help.md) in [Preparazione di Active Directory e dei domini](prepare-active-directory-and-domains-exchange-2013-help.md).

Una volta che Exchange ha terminato l'estensione dello schema, imposta la versione dello schema schema, che è archiviata nell'attributo **ms-Exch-Schema-Version-Pt**. Per accertarsi che lo schema Active Directory sia stato eseguito correttamente, è possibile controllare il valore archiviato in questo attributo. Se il valore dell'attributo corrisponde alla versione dello schema elencata per la versione di Exchange 2013 installata, l'estensione dello schema è riuscita. Per un elenco di versioni di Exchange e per sapere come controllare il valore di questo attributo, consultare la sezione [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) in [Preparazione di Active Directory e dei domini](prepare-active-directory-and-domains-exchange-2013-help.md).

## Preparare contenitori, oggetti e altri elementi di Active Directory

Con lo schema esteso, il passaggio successivo è aggiungere tutti i contenitori, gli oggetti e altri elementi utilizzati da Exchange per archiviare le informazioni in Active Directory. Gran parte delle modifiche apportate in questo passaggio vengono applicate all'intera foresta di Active Directory. Un insieme più piccolo di modifiche viene effettuato sul dominio locale di Active Directory in cui è stato eseguito il comando *PrepareAD* durante l'installazione.

Di seguito vengono indicate le modifiche apportate alla foresta di Active Directory:

  - Il contenitore di Microsoft Exchange viene creato in CN=Services,CN=Configuration,DC=\<*dominio radice*\> se non esiste già.

  - I seguenti contenitori e oggetti vengono creati in CN=\<*nome organizzazione*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*dominio radice*\> se non esistono già:
    
      - CN=Address Lists Container
    
      - CN=AddressBook Mailbox Policies
    
      - CN=Addressing
    
      - CN=Administrative Groups
    
      - CN=Approval Applications
    
      - CN=Auth Configuration
    
      - CN=Availability Configuration
    
      - CN=Client Access
    
      - CN=Connections
    
      - CN=ELC Folders Container
    
      - CN=ELC Mailbox Policies
    
      - CN=ExchangeAssistance
    
      - CN=Federation
    
      - CN=Federation Trusts
    
      - CN=Global Settings
    
      - CN=Hybrid Configuration
    
      - CN=Mobile Mailbox Policies
    
      - CN=Mobile Mailbox Settings
    
      - CN=Monitoring Settings
    
      - CN=OWA Mailbox Policies
    
      - CN=Provisioning Policy Container
    
      - CN=Push Notification Settings
    
      - CN=RBAC
    
      - CN=Recipient Policies
    
      - CN=Remote Accounts Policies Container
    
      - CN=Retention Policies Container
    
      - CN=Retention Policy Tag Container
    
      - CN=ServiceEndpoints
    
      - CN=System Policies
    
      - CN=Team Mailbox Provisioning Policies
    
      - CN=Transport Settings
    
      - CN=UM AutoAttendant Container
    
      - CN=UM DialPlan Container
    
      - CN=UM IPGateway Container
    
      - CN=UM Mailbox Policies
    
      - CN=Workload Management Settings

  - I seguenti contenitori e oggetti vengono creati in CN=Transport Settings, CN=\<*Nome organizzazione*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*dominio root*\> se non esistono già:
    
      - CN=Accepted Domains
    
      - CN=ControlPoint Config
    
      - CN=DNS Customization
    
      - CN=Interceptor Rules
    
      - CN=Malware Filter
    
      - CN=Message Classifications
    
      - CN=Message Hygiene
    
      - CN=Rules
    
      - CN=MicrosoftExchange329e71ec88ae4615bbc36ab6ce41109e

  - Le autorizzazioni vengono impostate in tutta la partizione di configurazione in Active Directory.

  - Il file Rights.ldf viene importato. Questo file aggiunge le autorizzazioni necessarie per installare Exchange e configurare Active Directory.

  - L'unità organizzativa Gruppi di protezione di Microsoft Exchange viene creata nel dominio radice della foresta e autorizzazioni vengono assegnate a tale unità.

  - I seguenti gruppi di ruoli di gestione vengono creati nell'unità organizzativa Gruppi di protezione di Microsoft Exchange se non esistono già:
    
      - Gestione della conformità
    
      - Installazione delegata
    
      - Gestione individuazione
    
      - Assistenza
    
      - Gestione di Hygiene
    
      - Gestione organizzazione
    
      - Gestione cartelle pubbliche
    
      - Gestione destinatari
    
      - Gestione record
    
      - Gestione server
    
      - Gestione messaggistica unificata
    
      - Gestione organizzazione sola visualizzazione

  - I nuovi gruppi di ruoli di gestione (che compaiono come gruppi di protezione universali (USG) in Active Directory) creati nell'unità organizzativa Gruppi di protezione di MicrosoftExchange vengono aggiunti all'attributo **otherWellKnownObjects** archiviato nel contenitore CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*dominio radice*\>.

  - Il contatto del mittente del messaggio vocale di messaggistica unificata viene creato nel contenitore Oggetti di sistema di Microsoft Microsoft Exchange del dominio radice.

  - Il dominio in cui viene eseguito il comando *PrepareAD* è preparato per Exchange 2013. Per informazioni sulle operazioni effettuate per preparare il dominio di Active Directory per Exchange, consultare Preparing Active Directory domains.

  - La proprietà **msExchProductId** dell'oggetto organizzazione Exchange è impostata. Per accertarsi che lo schema Active Directory sia stato eseguito correttamente, è possibile controllare il valore archiviato in questa proprietà. Se il valore nella proprietà corrisponde alla versione dello schema elencata per la versione di Exchange 2013 installata, l'estensione dello schema è riuscita. Per un elenco di versioni di Exchange e per sapere come controllare il valore di questa proprietà, consultare la sezione [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) in [Preparazione di Active Directory e dei domini](prepare-active-directory-and-domains-exchange-2013-help.md).

## Preparare i domini di Active Directory

Il passaggio finale della preparazione di Active Directory per Exchange è preparare tutti i domini di Active Directory in cui i server Exchange saranno installati o in cui saranno collocati gli utenti abilitati alle cassette postali. Questo passaggio viene effettuato automaticamente nel dominio in cui è stato eseguito il comando *PrepareAD*.

Di seguito vengono indicate le modifiche apportate ai domini di Active Directory:

  - Il contenitore Oggetti di sistema di Microsoft Exchange viene creato nella partizione del dominio radice in Active Directory se non esiste già.

  - Le autorizzazioni sono impostate nel contenitore Oggetti di sistema di Microsoft Exchange per i gruppi di protezione Utenti autenticati, Gestione organizzazione e Server di Exchange.

  - Il gruppo globale del dominio Exchange Install Domain Servers viene creato nel dominio corrente e collocato nel contenitore Oggetti di sistema di Microsoft Exchange.

  - Il gruppo Exchange Install Domain Servers è un membro del gruppo di protezione universale Server di Exchange nel dominio radice.

  - Le autorizzazioni vengono assegnate a livello del dominio per i gruppi di protezione universale (USG) Gestione organizzazione e Server di Exchange.

  - La proprietà **objectVersion** del contenitore Oggetti di sistema di Microsoft Exchange in DC=\<*dominio radice*\> viene impostata. Per accertarsi che lo schema Active Directory sia stato eseguito correttamente, è possibile controllare il valore archiviato in questa proprietà. Se il valore nella proprietà corrisponde alla versione dello schema elencata per la versione di Exchange 2013 installata, l'estensione dello schema è riuscita. Per un elenco di versioni di Exchange e per sapere come controllare il valore di questa proprietà, consultare la sezione [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) in [Preparazione di Active Directory e dei domini](prepare-active-directory-and-domains-exchange-2013-help.md).


---
title: 'Multi-tenancy in Exchange 2013: Exchange 2013 Help'
TOCTitle: Multi-tenancy in Exchange 2013
ms:assetid: df09257d-dd98-4f59-b830-1818cedda15c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ862352(v=EXCHG.150)
ms:contentKeyID: 50555702
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Multi-tenancy in Exchange 2013

 

_**Si applica a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Una distribuzione di Exchange 2013 multi-tenant (ospitata) viene definita come una distribuzione in cui l'organizzazione di Exchange viene configurata per ospitare più organizzazioni o business unit distinte (i tenant) che normalmente non condividono messaggi di posta elettronica, dati, utenti, elenchi indirizzi globali o altri oggetti di Exchange di uso comune. La condivisione di hardware, software e risorse (mantenendo contemporaneamente una separazione logica tra tenant) consente alle organizzazioni di sfruttare la semplicità di una distribuzione di Exchange standard fornendo nel contempo funzionalità multi-tenant e servizi che soddisfino le esigenze di hosting.

## Funzionalità multi-tenancy nelle organizzazioni di Exchange 2013

In Exchange 2013 è continuano a supportare l'hosting con una standard, installazione di Exchange locale simile a quella utilizzata in Exchange 2010 Service Pack 2 (SP2). Vengono sospese l'opzione modalità `/hosting` e, stanno evidenziando l'utilizzo dei criteri della Rubrica (criteri della Rubrica) in combinazione con hosting di soluzioni per la gestione e automation strumenti forniti da approvato fornitori di Software indipendenti (ISV). Queste soluzioni sono basate su una struttura di approvazione Microsoft configurazione linee guida e procedure consigliate e saranno disponibili le organizzazioni di Exchange di offrire funzionalità e servizi di hosting in modo più semplice e più affidabile.

Exchange 2013 supporta multi-tenancy sfruttando le funzionalità e i componenti seguenti principali:

  - **Active Directory**   Invece di avere contenitori separati di *ExchangeOrganization* Active Directory per ciascuna business unit in un'organizzazione di Exchange multi-tenant, la funzionalità multi-tenancy di Exchange 2013 è supportata utilizzando un singolo contenitore di *ExchangeOrganization* Active Directory. In questo modo viene semplificata la struttura di Active Directory e ridotta la probabilità di problemi di autorizzazioni legati ad Active Directory.
    
    Per ulteriori informazioni sulle modifiche di Active Directory in Exchange 2013, vedere [Active Directory](active-directory-exchange-2013-help.md).

  - **Criteri delle rubriche (criteri della Rubrica)**   Introdotto in Exchange 2010 Service Pack 2, vengono utilizzati criteri della Rubrica in Exchange 2013 per controllare l'accesso a un elenco di indirizzi, elenchi di indirizzi globale (GAL) e un rubriche non in linea (rubriche offline) nell'organizzazione di Exchange. Criteri della Rubrica raggruppare i diversi oggetti di Active Directory in un oggetto virtuale che può essere assegnato ai singoli utenti e per creare un raggruppamento logico di tali risorse lungo una struttura dell'organizzazione multi-tenant. Funzionalità di criterio della Rubrica in Exchange 2013 è simile a era in Exchange 2010 SP2.
    
    Per ulteriori informazioni sui criteri della rubrica in Exchange 2013, vedere [Criteri delle rubriche](https://docs.microsoft.com/it-it/exchange/address-books/address-book-policies/address-book-policies).

  - **Soluzioni di gestione hosting**   Alcuni amministratori che utilizzano Exchange 2013 per fornire una soluzione di Exchange ospitata trarranno vantaggio dall'utilizzo di un approccio di gestione hosting personalizzato. A causa di alcune limitazioni di Interfaccia di amministrazione di Exchange, Microsoft collabora con fornitori di terze parti per fornire assistenza nello sviluppo del pannello di controllo e nelle soluzioni di automazione conformi alle linee guida e al framework approvato per le organizzazioni ospitate di Exchange 2013. Si consiglia alle organizzazioni che configurano una soluzione Exchange ospitata di sfruttare questi strumenti per gestire le proprie organizzazioni ospitate, ove richiesto.
    
    Per ulteriori informazioni sulla gestione ospitato soluzioni, inclusi i fornitori di soluzione convalidato, vedere [hosting di Exchange Server 2013 e soluzioni di multi-tenancy e istruzioni](https://go.microsoft.com/fwlink/?linkid=275036)


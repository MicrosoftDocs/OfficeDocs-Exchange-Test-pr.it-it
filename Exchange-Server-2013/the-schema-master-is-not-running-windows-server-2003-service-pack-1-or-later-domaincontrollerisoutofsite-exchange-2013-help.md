---
title: 'Master schema non è in esecuzione Windows Server 2003 Service Pack 1 o later_DomainControllerIsOutOfSite: Exchange 2013 Help'
TOCTitle: Master schema non è in esecuzione Windows Server 2003 Service Pack 1 o later_DomainControllerIsOutOfSite
ms:assetid: 5edbe0b8-7610-4a52-aaaa-38c6a99e7e53
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.domaincontrollerisoutofsite(v=EXCHG.150)
ms:contentKeyID: 50480728
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Master schema non è in esecuzione Windows Server 2003 Service Pack 1 o later\_DomainControllerIsOutOfSite

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2007 non può continuare l'installazione perché assegnato al controller di dominio Active Directory directory servizio ruolo master schema, noti anche come singolo master operazioni FSMO, non è in esecuzione Microsoft Windows Server 2003 Service Pack 1 (SP1) o versione successiva.

Installazione di Exchange 2007 richiede che il controller di dominio che funge da FSMO dello schema eseguito Windows Server 2003 SP1 o versione successiva.

Consente di controllare FSMO di tutti gli aggiornamenti e le modifiche allo schema di Active Directory.

Per risolvere questo problema, eseguire una o più delle operazioni seguenti:

  - Aggiornare il controller di dominio FSMO per Windows Server 2003 SP1 o versione successiva e rieseguire il programma di installazione di Microsoft Exchange.

  - Se non vi è un controller di dominio FSMO che esegue Microsoft Windows Server 2003 Service Pack 1 (SP1) o versione successiva nell'organizzazione di Exchange, eseguire il programma di installazione di Exchange 2007 con il parametro /domaincontroller che punta al controller di dominio FSMO:
    
    \[*/DomainController*o */dc\<FQDN of domain controller\>*\]
    
    Utilizzare il parametro */DomainController* per specificare il controller di dominio da utilizzare per leggere e scrivere in Active Directory durante l'installazione. È possibile utilizzare nome NetBIOS o il formato di nome di dominio completo (FQDN) di nome.

Per ottenere il service pack più recente per Windows Server 2003, vedere "TechCenter di Windows Server" ([https://go.microsoft.com/fwlink/?LinkId=45315](https://go.microsoft.com/fwlink/?linkid=45315)).

Per ulteriori informazioni sui parametri di installazione di Exchange Server 2007, vedere "Come per installare Exchange 2007 in modalità automatica" ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476)) nella documentazione del prodotto Exchange Server 2007.


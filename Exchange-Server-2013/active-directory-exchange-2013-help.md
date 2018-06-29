---
title: 'Active Directory: Exchange 2013 Help'
TOCTitle: Active Directory
ms:assetid: 8e8464df-2d1d-4d68-82de-b0c158c549c3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123715(v=EXCHG.150)
ms:contentKeyID: 50481157
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Microsoft Exchange Server 2013 utilizza Active Directory per archiviare e condividere le informazioni della directory con Windows. La struttura della foresta di Active Directory per Exchange 2013 è simile a quella di Exchange Server 2010, tranne per alcuni aspetti affrontati di seguito.

## Driver di Active Directory

La dipendenza Active Directory è il componente Exchange Microsoft core consente servizi Exchange creare, modificare, eliminare e query per Active Directory dati di servizi di dominio (AD DS). In Exchange 2013 completamente l'accesso a Active Directory viene eseguita utilizzando il driver Active Directory stesso. In precedenza, in Exchange 2010 DSAccess disponibili servizi di ricerca nella directory per i componenti, ad esempio SMTP, agente trasferimento messaggi () e l'archivio Exchange.

Il driver Active Directory utilizza inoltre Microsoft ExchangeActive Directory topologia (MSExchangeADTopology), che consente il driver Active Directory utilizzare i dati di topologia di accesso al servizio Directory (DSAccess). Questi dati includono l'elenco di controller di dominio disponibile e server di catalogo globale disponibile per gestire le richieste Exchange. Per ulteriori informazioni su Active Directory Driver, vedere [Servizi di dominio Active Directory](https://go.microsoft.com/fwlink/p/?linkid=110942).

## modifiche dello schema in Active Directory

In Exchange 2013 sono stati aggiunti nuovi attributi allo schema dei servizi di dominio di Active Directory e sono state apportate anche altre modifiche alle classi e agli attributi esistenti. Per ulteriori informazioni sulle modifiche ad Active Directory durante l'installazione di Exchange 2013, vedere [Modifiche allo schema di Active Directory in Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

## Ulteriori informazioni

Per saperne di più sul modo in cui Exchange 2013 archivia e recupera le informazioni in Active Directory al fine di poter pianificare gli accessi, vedere [Accesso ad Active Directory](access-to-active-directory-exchange-2013-help.md).

Per ulteriori informazioni sulla progettazione di un insieme di strutture Active Directory, vedere [Guida alla progettazione di AD DS](https://go.microsoft.com/fwlink/p/?linkid=264957).

Per saperne di più sui computer con sistema operativo Windows in un dominio Active Directory e sulla distribuzione di Exchange 2013 in un dominio con uno spazio dei nomi disgiunto, vedere [Scenari di spazio dei nomi disgiunto](disjoint-namespace-scenarios-exchange-2013-help.md).


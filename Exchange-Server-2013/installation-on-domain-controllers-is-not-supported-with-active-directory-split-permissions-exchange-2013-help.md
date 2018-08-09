---
title: 'Instal. controller dominio non supportata con autorizz. AD: Exchange 2013 Help'
TOCTitle: Installazione nei controller di dominio non è supportata con di Active Directory le autorizzazioni
ms:assetid: 977e3758-5e09-40a2-80c1-fe344b1d8a2a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.installondcinadsplitpermissionmode(v=EXCHG.150)
ms:contentKeyID: 50481228
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installazione nei controller di dominio non è supportata con di Active Directory le autorizzazioni

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-11-12_

Il programma di installazione di Microsoft Exchange Server 2013 ha rilevato il tentativo di eseguire il programma di installazione su un controller di dominio Active Directory e si è verificata una delle seguenti condizioni:

  - L'organizzazione di Exchange è già configurata per la suddivisione delle autorizzazioni di Active Directory.

  - È stata selezionata l'opzione di suddivisione delle autorizzazioni di Active Directory nel programma di installazione di Exchange 2013.

L'installazione di Exchange 2013 nei controller di dominio non è supportata quando l'organizzazione di Exchange è configurata per la suddivisione delle autorizzazioni di Active Directory.

Se si desidera installare Exchange 2013 in un controller di dominio, è necessario configurare l'organizzazione di Exchange per la suddivisione delle autorizzazioni RBAC (Role Based Access Control) o per la condivisione delle autorizzazioni.


> [!IMPORTANT]
> Si consiglia di non installare Exchange 2013 nei controller di dominio di Active Directory. Per ulteriori informazioni, vedere <A href="installing-exchange-on-a-domain-controller-is-not-recommended-exchange-2013-help.md">Installazione di Exchange in un controller di dominio non è consigliabile</A>.



Se si desidera continuare a utilizzare la suddivisione delle autorizzazioni di Active Directory, è necessario installare Exchange 2013 in un server membro.

Per ulteriori informazioni sulla suddivisione e condivisione delle autorizzazioni in Exchange 2013, vedere i seguenti argomenti:

[Informazioni sulle autorizzazioni diviso](understanding-split-permissions-exchange-2013-help.md)

[Configurare Exchange 2013 per le autorizzazioni diviso](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)

[Configurare Exchange 2013 per autorizzazioni condivise](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


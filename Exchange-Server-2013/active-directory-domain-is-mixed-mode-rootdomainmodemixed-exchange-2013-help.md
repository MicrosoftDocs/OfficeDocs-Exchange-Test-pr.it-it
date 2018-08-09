---
title: 'Dominio AD modalità mista_RootDomainModeMixed: Exchange 2013 Help'
TOCTitle: Mode_RootDomainModeMixed combinazione di dominio Active Directory
ms:assetid: 9f60096e-3eaa-40d8-bde5-13ada5855702
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.rootdomainmodemixed(v=EXCHG.150)
ms:contentKeyID: 50481303
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mode\_RootDomainModeMixed combinazione di dominio Active Directory

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Il programma di installazione di Microsoft® Exchange Server 2007 non può continuare perché un dominio di Active Directory esistente non è impostato su modalità nativa Microsoft Windows® ° 2000 Server o dell'integrazione.

Installazione di Exchange 2007 creerà gruppi di protezione universali che è disponibile solo in modalità nativa Windows 2000 Server o, better, i domini.

Per risolvere questo problema, eseguire la procedura seguente per generare il livello funzionalità dominio livello per almeno il Windows 2000 Server nativo e quindi rieseguire il programma di installazione di Exchange 2007.

Per aumentare il livello funzionale di dominio

1.  Aprire domini e trust Active Directory.

2.  Nell'albero della console, destro del mouse sul dominio per cui si desidera elevare funzionalità e quindi fare clic su **Genera livello funzionale di dominio**.

3.  In **Selezionare un livello funzionale di dominio disponibile**, utilizzare una delle procedure seguenti:
    
      - Per aumentare il livello funzionale di dominio a nativo Windows 2000 Server, fare clic su **Windows 2000 nativo** e quindi fare clic su **Genera**.
    
      - Per aumentare il livello funzionale di dominio di Windows Server® 2003, fare clic su **Windows Server 2003** e quindi fare clic su **Genera.**


> [!WARNING]
> <BR>Se si dispone o disporrà di controller di dominio che eseguono Windows NT® 4.0 e versioni precedenti, genera il livello funzionale di dominio a nativo Windows 2000 Server. Dopo il livello funzionale di dominio è impostato su nativo Windows 2000 Server, non è possibile modificarlo al misto Windows 2000 Server.<BR>Se o verrà qualsiasi controller di dominio che eseguono Windows NT 4.0 o versioni precedenti oppure Windows 2000 Server, non aumentare il livello funzionale di dominio a Windows Server 2003. Dopo aver impostato il livello funzionale di dominio a Windows Server 2003, non è possibile modificarlo in Windows Server 2000 misto o nativo Windows 2000 Server.



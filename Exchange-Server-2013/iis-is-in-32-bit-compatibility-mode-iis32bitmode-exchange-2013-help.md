---
title: 'IIS è in mode_IIS32BitMode compatibilità a 32 bit: Exchange 2013 Help'
TOCTitle: IIS è in mode_IIS32BitMode compatibilità a 32 bit
ms:assetid: 742dfc32-353c-46a2-830e-68aed6a68ce0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.iis32bitmode(v=EXCHG.150)
ms:contentKeyID: 50480985
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS è in mode\_IIS32BitMode compatibilità a 32 bit

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Poiché Microsoft Internet Information Service (IIS) è in esecuzione in modalità a 32 bit su questo computer a 64 bit, non continuare l'installazione di Microsoft® Exchange Server 2007.

Exchange 2007 è necessario che IIS sia in modalità a 64 bit quando viene eseguito in un computer a 64 bit.

Per risolvere questo problema, passare IIS alla modalità a 64 bit e quindi rieseguire il programma di installazione di Microsoft Exchange.

Per passare IIS alla modalità a 64 bit

1.  Aprire una finestra con il prompt dei comandi.

2.  Digitare il comando seguente:
    
    **cscript c:\\inetpub\\adminscripts\\adsutil.vbs SET /w3svc/AppPools/Enable32BitAppOnWin64 False**

3.  Premere INVIO


---
title: 'Impossibile determinare il nome di site_InvalidADSite Active Directory: Exchange 2013 Help'
TOCTitle: Impossibile determinare il nome di site_InvalidADSite Active Directory
ms:assetid: ef96e077-08a0-4108-9f7d-0d61758abcd4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.invalidadsite(v=EXCHG.150)
ms:contentKeyID: 50481992
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impossibile determinare il nome di site\_InvalidADSite Active Directory

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Perché questo server non appartenga a un sito di servizi di directory Active Directory® valido, non continuare l'installazione di Microsoft® Exchange Server 2007.

Il programma di installazione di Microsoft Exchange richiede che il server utilizzato per l'installazione di Exchange 2007 appartenga a un sito di Active Directory valido.

Per risolvere questo problema, verificare che il server locale sia un membro di un sito di Active Directory valido e rieseguire il programma di installazione di Exchange Server 2007.

È possibile utilizzare l'opzione **/DsGetSite** dello strumento da riga di comando Nltest.exe per verificare e visualizzare l'appartenenza ai siti. Per ulteriori informazioni, vedere "Nltest.exe: NLTest Overview" in "Strumenti e le impostazioni di insieme" di *Documentazione tecnica di Windows Server 2003* ([https://go.microsoft.com/fwlink/?LinkId=27734](https://go.microsoft.com/fwlink/?linkid=27734)).

Per ulteriori informazioni sulla risoluzione dei problemi di Active Directory, vedere "Risoluzione dei problemi relativi alle operazioni di Active Directory" in *Windows Server 2003: operazioni di* (<https://go.microsoft.com/fwlink/?linkid=68099>).


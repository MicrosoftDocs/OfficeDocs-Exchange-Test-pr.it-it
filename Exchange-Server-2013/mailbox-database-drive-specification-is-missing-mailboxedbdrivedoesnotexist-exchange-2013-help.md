---
title: 'Specifica unità del database delle cassette postali è missing_MailboxEDBDriveDoesNotExist: Exchange 2013 Help'
TOCTitle: Specifica unità del database delle cassette postali è missing_MailboxEDBDriveDoesNotExist
ms:assetid: 0e487aa1-3194-4a14-b255-a8b9f9afbf0e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.mailboxedbdrivedoesnotexist(v=EXCHG.150)
ms:contentKeyID: 50479991
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Specifica unità del database delle cassette postali è missing\_MailboxEDBDriveDoesNotExist

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Ripristino di emergenza di Microsoft® Exchange Server 2007 non può proseguire con l'installazione perché il programma di installazione di ripristino di emergenza non può accedere alla cassetta postale specifica unità utilizzato nell'installazione precedente del server del database.

Il programma di installazione di Microsoft Exchange Disaster Recovery è necessario che le stesse specifiche unità del database delle cassette postali precedentemente utilizzate per il server sia disponibile durante il ripristino.

Per risolvere questo problema, configurare le unità in base alla configurazione di unità logica originale e rieseguire il programma di installazione di Microsoft Exchange Disaster Recovery.

Assegnare o modificare una lettera di unità

1.  Aprire **Gestione Computer(locale)**.

2.  Nell'albero della console, fare clic su **Gestione Computer (locale)**, fare clic su **archiviazione** e quindi fare clic su **Gestione disco**.

3.  Destro una partizione, unità logiche o volume e quindi fare clic su **percorsi e lettera di unità di modifica**.

4.  Utilizzare le procedure illustrate di seguito:
    
      - Per assegnare una lettera di unità, fare clic su **Aggiungi**, selezionare la lettera di unità che si desidera utilizzare e quindi fare clic su **OK**.
    
      - Per modificare una lettera di unità, selezionarlo, fare clic su **Modifica** e quindi fare clic su **OK** la lettera di unità da utilizzare.

Per ulteriori informazioni su come assegnare lettere di unità, vedere "Assegnazione, modificare o rimuovere una lettera di unità" ([https://go.microsoft.com/fwlink/?LinkId=66764](https://go.microsoft.com/fwlink/?linkid=66764)).


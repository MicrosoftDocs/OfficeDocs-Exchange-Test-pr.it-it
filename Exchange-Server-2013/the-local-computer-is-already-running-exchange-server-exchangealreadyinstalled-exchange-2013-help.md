---
title: 'Nel computer locale è già in esecuzione Exchange Server_ExchangeAlreadyInstalled: Exchange 2013 Help'
TOCTitle: Nel computer locale è già in esecuzione Exchange Server_ExchangeAlreadyInstalled
ms:assetid: 3f168b5d-9910-418f-86fb-e99d852dcb5e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.exchangealreadyinstalled(v=EXCHG.150)
ms:contentKeyID: 50480478
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Nel computer locale è già in esecuzione Exchange Server\_ExchangeAlreadyInstalled

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Non può continuare l'installazione di Microsoft® Exchange Server 2007 nel computer locale sia installati componenti precedenti di Microsoft Exchange.

Installazione di Exchange 2007 è necessario che nel computer locale non è installati esistenti componenti di Microsoft Exchange.

Per risolvere questo problema, rimuovere i componenti di Microsoft Exchange 2000 Server o Microsoft Exchange Server 2003 e quindi rieseguire il programma di installazione di Microsoft Exchange.

Per rimuovere i componenti di Microsoft Exchange

1.  Fare clic su **Start**, scegliere **Impostazioni** e quindi fare clic su **Pannello di controllo**.

2.  Fare doppio clic su **Installazione applicazioni**.

3.  Nell'elenco **Programmi attualmente installati** fare clic su **Microsoft Exchange** e quindi fare clic su **Cambia/Rimuovi**.

4.  Nell'installazione guidata di Microsoft Exchange, fare clic su **Avanti**.

5.  Nella colonna azione nella pagina Selezione componenti, fare clic sulla freccia in giù accanto a ogni componente di cui è stato installato e quindi fare clic su **Rimuovi**.
    

    > [!NOTE]
    > Componenti installati dispongono di un segno di spunta nella colonna azione. Quando si fa clic su <STRONG>Rimuovi</STRONG>, il segno di spunta viene sostituito da word <STRONG>rimuovere</STRONG>.



6.  Fare clic su **Avanti** due volte.

7.  Fare clic su **Fine**.


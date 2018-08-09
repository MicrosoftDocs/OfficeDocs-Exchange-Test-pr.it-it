---
title: 'PC controller dominio sec._LocalComputerIsDCInChildDomain:Exchange 2013 Help'
TOCTitle: Il computer locale è un controller di dominio di un domain_LocalComputerIsDCInChildDomain figlio
ms:assetid: 7db1dcc0-d953-41b8-b081-2a47a70950c4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.localcomputerisdcinchilddomain(v=EXCHG.150)
ms:contentKeyID: 50481043
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Il computer locale è un controller di dominio di un domain\_LocalComputerIsDCInChildDomain figlio

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Dal momento che il computer locale è un controller di dominio per un dominio figlio, non può continuare l'installazione di Microsoft® Exchange Server 2007.

Installazione di Exchange 2007 non verrà effettuata a un controller di dominio per un dominio figlio a meno che il controller di dominio è un server di catalogo globale.

Per risolvere questo problema, promuovere il controller di dominio a un server di catalogo globale o installazione di Exchange 2007 a un controller di dominio non, il dominio figlio, un server membro e quindi rieseguire il programma di installazione di Microsoft Exchange.

Per risolvere il problema rendendo il server di Exchange server di catalogo globale

1.  Nel controller di dominio, fare clic su **Start**, scegliere **programmi**, fare clic su **Strumenti di amministrazione** e quindi fare clic su **siti di Active Directory e i servizi**.

2.  Nell'albero della console, fare doppio clic su **siti**, fare doppio clic sul nome del sito e fare doppio clic sul **server**.

3.  Fare doppio clic sul controller di dominio di destinazione.

4.  Nel riquadro dei risultati **Impostazioni NTDS** pulsante destro del mouse e quindi scegliere **proprietà**.

5.  Nella scheda **Generale**, fare clic per selezionare la casella di controllo di **catalogo globale**.

6.  Riavviare il controller di dominio.

